QtRaspberry
====
Hi everyone,
I made a tutorial about Serial Communication between Rapberry and devices (ESP32, Arduino) implemented with Qt and multithreading.
It is shown als how to implement a simple communication protocol for applications where large amount of information are needed.

You can see it on

[youtube](https://youtu.be/AFJxrrIvZrU)

Source code is available on

[github](https://github.com/vigasan/SerialCom.git)

## Singleton
  The version that fully supports singletons is [v5.14+](https://doc.qt.io/qt-5/qqmlengine.html#qmlRegisterSingletonType-2)    
  This function was introduced in Qt 5.14.
```c++
template <typename T> int qmlRegisterSingletonType(const char *uri, int versionMajor, int versionMinor, const char *typeName, 
std::function<QObject *(QQmlEngine *, QJSEngine *)> callback)
```
  主要的改进是第5个参数！ 之前，是实例不了带参的类的。    
  The main improvement is the fifth parameter! Previously, only classes with no parameters could be instantiated.    
  Example for v5.12: [qml-cpp-integration-example](https://github.com/RaymiiOrg/qml-cpp-integration-example/pull/1/commits/07d82aeea2ed9971fb6a4c61d0ce8a691824ca6e)
```c++
qmlRegisterSingletonType<TrafficLightClass>("org.raymii.RoadObjects", 1, 0, "TrafficLightSingleton",
                                     [](QQmlEngine *engine, QJSEngine *scriptEngine) -> QObject * {
        Q_UNUSED(engine)
        Q_UNUSED(scriptEngine)

        TrafficLightClass *trafficLightSingleton = new TrafficLightClass();
        return trafficLightSingleton;
    });
```
  Example for v5.14+: [qml-cpp-integration-example](https://raymii.org/s/articles/Qt_QML_Integrate_Cpp_with_QML_and_why_ContextProperties_are_bad.html)
```c++
 TrafficLightClass trafficLightSingleton;
    qmlRegisterSingletonType<TrafficLightClass>("org.raymii.RoadObjects", 1, 0, "TrafficLightSingleton",
                                     [&](QQmlEngine *, QJSEngine *) -> QObject * {
        return &trafficLightSingleton;
    });
```

## Ref
- [Qt and Serial Communication Tutorial](https://forums.raspberrypi.com/viewtopic.php?t=304199)
