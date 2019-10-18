# Java Byte Code Level Method Invoker


## 实例

```java

public class TestHandlerInvoker {

    public static void main(String[] args) throws Exception {

        System.setProperty("cglib.debugLocation", "D:/debug");
        {
            final Method main = Bean.class.getDeclaredMethod("main");
            final Invoker mainInvoker = MethodInvokerCreator.create(main);

            mainInvoker.invoke(null, null);
        }
        {
            final Method test = Bean.class.getDeclaredMethod("test", short.class);

            final Invoker mainInvoker = MethodInvokerCreator.create(test);

            mainInvoker.invoke(null, new Object[] { (short) 1 });
        }

        final Invoker create = MethodInvokerCreator.create(Bean.class, "test");

        create.invoke(new Bean(), null);

        final Invoker itself = MethodInvokerCreator.create(Bean.class, "test", Bean.class);

        itself.invoke(new Bean(), new Object[] { new Bean() });
    }

    public static class Bean {

        public static void test(short i) {
            System.err.println("static main " + i);
        }

        public static void main() {
            System.err.println("static main");
        }

        public void test() {
            System.err.println("instance test");
        }

        public void test(Bean itself) {
            System.err.println("instance test :" + itself);
        }

    }
}

```