if get_option('tests')

  test_env = ['G_DEBUG=gc-friendly,fatal-warnings', 'MALLOC_CHECK_=2', 'NO_AT_BRIDGE=1']

  test_cflags = ['-DTEST_DATA_DIR="@0@"'.format(meson.current_source_dir() / 'data')]

  tests = ['cutout', 'display-panel', 'svg-path', 'timeout', 'utils', 'device-tree']
  # These need data not available on the installed system:
  not_installed = ['test-device-tree']

  foreach test : tests

    test_name = 'test-@0@'.format(test)
    test_conf = configuration_data()
    test_conf.set('installed_tests_dir', installed_tests_execdir)
    test_conf.set('program', test_name)
    test_conf.set('program', test_name)

    if get_option('installed_tests') and test_name not in not_installed
      configure_file(
        input: files('template.test.in'),
        output: test_name + '.test',
        install_dir: installed_tests_metadir,
        configuration: test_conf,
      )
    endif

    t = executable(
      test_name,
      ['test-@0@.c'.format(test)],
      c_args: test_cflags,
      pie: true,
      link_with: gm_lib,
      dependencies: gmobile_dep,
      install: get_option('installed_tests'),
      install_dir: installed_tests_execdir,
    )
    test(test, t, env: test_env)
  endforeach

endif
