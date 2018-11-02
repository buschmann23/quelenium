set(quelenium_SRC
    actions.cpp
    alert.cpp
    by.cpp
    cookie.cpp
    desiredcapabilities.cpp
    imehandler.cpp
    keys.cpp
    logentry.cpp
    logs.cpp
    mouse.cpp
    navigation.cpp
    options.cpp
    proxy.cpp
    select.cpp
    seleniumserverhub.cpp
    server.cpp
    targetlocator.cpp
    timeouts.cpp
    touch.cpp
    webdriver.cpp
    webdriverexception.cpp
    webdriverhub.cpp
    webelement.cpp
    window.cpp
)

set(quelenium_HEADERS
    actions.h
    alert.h
    browser.h
    by.h
    cookie.h
    desiredcapabilities.h
    imehandler.h
    keys.h
    logentry.h
    logs.h
    mouse.h
    navigation.h
    options.h
    platform.h
    proxy.h
    queleniumexception.h
    responsestatuscodes.h
    select.h
    seleniumserverhub.h
    server.h
    targetlocator.h
    timeouts.h
    touch.h
    unexpectedalertbehaviour.h
    webdriverexception.h
    webdriver.h
    webdriverhub.h
    webelement.h
    window.h
)

# convenience headers
set(quelenium_CONVHEADERS
    ../BrowserType
    ../DesiredCapabilities
    ../Keys
    ../Proxy
    ../QueleniumException
    ../WebDriver
    ../WebDriverException
)

add_library(quelenium SHARED
    ${quelenium_SRC}
    ${quelenium_HEADERS}
)

add_library(Quelenium ALIAS quelenium)

target_include_directories(quelenium
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
        $<INSTALL_INTERFACE:include/Quelenium/selenium>
    PRIVATE
        ${CMAKE_CURRENT_BINARY_DIR}
)

set_target_properties(quelenium PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION 0
)

target_link_libraries(quelenium
    PUBLIC
        Qt5::Core
        Qt5::Network
)

set_property(TARGET quelenium PROPERTY PUBLIC_HEADER ${quelenium_HEADERS})

install(TARGETS quelenium
    EXPORT QueleniumTargets DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION include/Quelenium/selenium
)

install(FILES ${quelenium_CONVHEADERS} DESTINATION include/Quelenium)
