project('glfw', ['c', 'cpp'],
    default_options : [
        'cpp_std=c++17'
    ]
)

glfw_dep = dependency('glfw3', required : false)

if not glfw_dep.found()
    sources = []
    dependencies = []
    args = []

    if host_machine.system() == 'darwin'
        add_languages('objc')

        dependencies += dependency('appleframework', modules : [ 'Cocoa', 'IOKit', 'CoreFoundation' ])

        sources += [
            'src/cocoa_init.m',
            'src/cocoa_joystick.m',
            'src/cocoa_monitor.m',
            'src/cocoa_window.m',
            'src/cocoa_time.c',
            'src/posix_thread.c',
            'src/nsgl_context.m',
            'src/egl_context.c',
            'src/osmesa_context.c'
        ]

        args += '-D_GLFW_COCOA'
    elif host_machine.system() == 'windows'
        sources += [
            'src/win32_init.c',
            'src/win32_joystick.c',
            'src/win32_monitor.c',
            'src/win32_time.c',
            'src/win32_thread.c',
            'src/win32_window.c',
            'src/wgl_context.c',
            'src/egl_context.c',
            'src/osmesa_context.c'
        ]

        args += '-D_GLFW_WIN32'
    elif host_machine.system() == 'linux'
        sources += [
            'src/x11_init.c',
            'src/x11_monitor.c',
            'src/x11_window.c',
            'src/xkb_unicode.c',
            'src/posix_time.c',
            'src/posix_thread.c',
            'src/glx_context.c',
            'src/egl_context.c',
            'src/osmesa_context.c'
        ]

        args += '-D_GLFW_X11'
    endif

    sources += [
        'src/context.c',
        'src/init.c',
        'src/input.c',
        'src/monitor.c',
        'src/vulkan.c',
        'src/window.c'
    ]

    libglfw = library('glfw3', sources,
        include_directories : include_directories('include'),
        dependencies : dependencies,
        c_args : args,
        cpp_args : args,
        objc_args : args,
        objcpp_args : args
    )

    glfw_dep = declare_dependency(
        link_with : libglfw,
        include_directories : include_directories('include')
    )
endif