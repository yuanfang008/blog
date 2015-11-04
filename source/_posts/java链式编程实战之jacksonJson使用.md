title: java链式编程实战之jacksonJson使用
date: 2015-11-04 18:50:18
categories: 后台
tags: java,后台
keywords: java,链式编程,后台开发
description: 本文主要谈谈链式编程和JacksonJson工具的使用。以下DEMO实现了对List对象集合属性的过滤，使用java实现。
---

> 本文主要谈谈链式编程和JacksonJson工具的使用。以下DEMO实现了对List对象集合属性的过滤，使用java实现。先上代码先：

```java

//对传入的对象集合进行属性过滤
public final class EnhanceList<L extends EnhanceList> extends ArrayList{

    public L removeBeanAttr(String beanAttr){
        return removeBeanAttributes(this,beanAttr);
    }

    public L  removePageInfo(List list,Class t){
        Field fields[] = t.getDeclaredFields();
        List attributes = new ArrayList();
        for (int i = 0; i < fields.length; i++) {
            attributes.add(fields[i].getName());
        }
        return removeBeanAttributes(list!=null ? list : this,attributes.toArray());
    }

    public L  removeBeanAttributes(List list,Object...beanAttr){
        try {
            if (!list.isEmpty() && beanAttr.length > 0){
                List subList = new EnhanceList();
                for (Object object:list){
                    Map map = (object instanceof Map) ? (Map) object : JacksonJSONUtil.object2Map(object);
                    for (int i = 0; i < beanAttr.length; i++) {
                        map.remove(beanAttr[i]);
                    }
                    subList.add(map);
                }
                return (L)subList;
            }
        }catch (Exception e){
            e.printStackTrace();
        }
        return (L)list;
    }

}

//JacksonJson工具类使用
public class JacksonJSONUtil {

    private static ObjectMapper mapper = new ObjectMapper();

    public static String toJsonString(Object object){
        try {
            StringWriter writer = new StringWriter();
            JsonGenerator jsonGenerator = mapper.getFactory().createGenerator(writer);
            jsonGenerator.writeObject(object);
            return writer.toString();
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }

    public static Map parseStringToMap(String string){
        return (Map)readObjectValue(string, Map.class);
    }

    public static Map object2Map(Object object){
        return (Map)readObjectValue(object, Map.class);
    }

    public static Object map2Object(Map map,Object object){
        return readObjectValue(map,object.getClass());
    }

    private static Object readObjectValue(Object object,Class clazz){
        try {
            if (object instanceof String) {
                return mapper.readValue((String) object, clazz);
            }else{
                byte bytes[] = mapper.writeValueAsBytes(object);
                return mapper.readValue(bytes, clazz);
            }
        } catch (Exception e) {
            e.printStackTrace();
            return object;
        }
    }
}

```

### 链式编程简述
所谓链式，也就是每次调用对象方法后返回的都是该对象本身，而该对象又可以继续调用方法。表现形式为`new EnhanceList().removeBeanAttr("a").removeBeanAttr("b").removeBeanAttr("c")`。
由于要返回对象本身，而类名不能直接返回。所以需要借助泛型实现。使用泛型还有一个好处是，即使是子类也无妨。

  以上便是链式编程案例和JacksonJson工具类的用法，至于为什么要用JacksonJson做解析，而不是jsonLib或fastJson。
  度娘是这样说的：JacksonJson使用流的方式处理json解析，速度会占优势。随着数据量的增大，JacksonJson表现也很稳定。性能最差的jsonLib应该是追求性能要避免的。
