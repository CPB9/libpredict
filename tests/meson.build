inc = include_directories('../include')

dummy = executable('dummy-t',
  sources : 'dummy-t.c',
  include_directories : inc,
)
test('dummy', dummy)

link = executable('link-t',
  sources : 'link-t.c',
  link_with : predict_lib,
  include_directories : inc,
)
test('link', link)

testcate_reader_lib = static_library('testcasereader',
  sources : 'testcase_reader.cpp',
)

test_runners = [
  'orbit',
  'aoslos',
  'sun',
  'moon',
  'maxelevation',
  'geostationary',
]

foreach runner : test_runners
  t = executable(runner,
    sources : runner + '-t.cpp',
    link_with : [predict_lib, testcate_reader_lib],
    include_directories : inc,
    cpp_args : predict_cflags,
  )
  set_variable(runner, t)
endforeach

sat_data = [
  'data/sat_ERS-1_201509261800.test',
  'data/sat_HINODE_201509261800.test',
  'data/sat_MOLNIYA_1-29_201509261800.test',
  'data/sat_THOR_III_201509261800.test',
  'data/sat_GPS_BIIA-10_201509261800.test',
  'data/sat_ISS_201509261800.test',
  'data/sat_SIRIUS-1_201509261800.test',
  'data/sat_VELA-1_201509261800.test',
]

foreach data : sat_data
  path = join_paths(meson.current_source_dir(), data)
  test('orbit_' + data, orbit, args : path)
  test('aoslos_' + data, aoslos, args : path)
  test('maxelevation_' + data, maxelevation, args : path)
endforeach

sun_data = [
  '../tests/data/sun_201509201933.test',
  '../tests/data/sun_201509210600.test',
]

foreach data : sun_data
  path = join_paths(meson.current_source_dir(), data)
  test('sun_' + data, sun, args : path)
endforeach

moon_data = [
  '../tests/data/moon_201509201000.test',
  '../tests/data/moon_201509201600.test',
]

foreach data : moon_data
  path = join_paths(meson.current_source_dir(), data)
  test('sun_' + data, moon, args : path)
endforeach

test('geostationary-celestrak-geostationary', geostationary,
  args: join_paths(meson.current_source_dir(), 'data', 'geostationary.tle')
)

test('geostationary-all-tles', geostationary,
  args: [join_paths(meson.current_source_dir(), 'data', 'large-tle-collection.tle'),
         join_paths(meson.current_source_dir(), 'data', 'geosynchronous_satellite_numbers.dat')],
)

