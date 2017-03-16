MACOS_CONFIG_H = """
#define GOOGLE_NAMESPACE ::google
#define HASH_FUN_H <functional>
#define HASH_MAP_H <unordered_map>
#define HASH_NAMESPACE std
#define HASH_SET_H <unordered_set>
#define HAVE_HASH_MAP 1
#define HAVE_HASH_SET 1
#define HAVE_INTTYPES_H 1
#define HAVE_LONG_LONG 1
#define HAVE_MEMCPY 1
#define HAVE_MEMMOVE 1
#define HAVE_MEMORY_H 1
#define HAVE_NAMESPACES 1
#define HAVE_STDINT_H 1
#define HAVE_STDLIB_H 1
#define HAVE_STRINGS_H 1
#define HAVE_STRING_H 1
#define HAVE_SYS_RESOURCE_H 1
#define HAVE_SYS_STAT_H 1
#define HAVE_SYS_TIME_H 1
#define HAVE_SYS_TYPES_H 1
#define HAVE_SYS_UTSNAME_H 1
#define HAVE_UINT16_T 1
#define HAVE_UNISTD_H 1
#define HAVE_UNORDERED_MAP 1
#define HAVE_U_INT16_T 1
#define PACKAGE \\"sparsehash\\"
#define PACKAGE_BUGREPORT \\"google-sparsehash@googlegroups.com\\"
#define PACKAGE_NAME "sparsehash"
#define PACKAGE_STRING \\"sparsehash 2.0.3\\"
#define PACKAGE_TARNAME \\"sparsehash\\"
#define PACKAGE_URL \\"\\"
#define PACKAGE_VERSION \\"2.0.3\\"
#define SPARSEHASH_HASH HASH_NAMESPACE::hash
#define SPARSEHASH_HASH_NO_NAMESPACE hash
#define STDC_HEADERS 1
#define VERSION \\"2.0.2\\"
#define _END_GOOGLE_NAMESPACE_ }
#define _START_GOOGLE_NAMESPACE_ namespace google {
"""

MACOS_SPARSE_CONFIG_H = """
#define GOOGLE_NAMESPACE ::google
#define HASH_FUN_H <functional>
#define HASH_NAMESPACE std
#define HAVE_INTTYPES_H 1
#define HAVE_LONG_LONG 1
#define HAVE_MEMCPY 1
#define HAVE_STDINT_H 1
#define HAVE_SYS_TYPES_H 1
#define HAVE_UINT16_T 1
#define HAVE_U_INT16_T 1
#define SPARSEHASH_HASH HASH_NAMESPACE::hash
#define _END_GOOGLE_NAMESPACE_ }
#define _START_GOOGLE_NAMESPACE_ namespace google {
"""

genrule(
  name = 'macos-config.h',
  out = 'config.h',
  cmd = 'echo "' + MACOS_CONFIG_H + '" > $OUT',
)

genrule(
  name = 'macos-sparseconfig.h',
  out = 'sparseconfig.h',
  cmd = 'echo "' + MACOS_SPARSE_CONFIG_H + '" > $OUT',
)

macos_headers = {
  'config.h': ':macos-config.h',
  'sparsehash/internal/sparseconfig.h': ':macos-sparseconfig.h',
}

prebuilt_cxx_library(
  name = 'sparsehash',
  header_only = True,
  header_namespace = '',
  exported_headers = subdir_glob([
    ('src', 'google/**/*'),
    ('src', 'sparsehash/**/*'),
  ]),
  exported_platform_headers = [
    ('default', macos_headers),
    ('^macos.*', macos_headers),
  ],
  visibility = [
    'PUBLIC',
  ],
)

cxx_binary(
  name = 'hashtable_test',
  srcs = [
    'src/hashtable_test.cc',
  ],
  deps = [
    ':sparsehash',
  ],
)

cxx_binary(
  name = 'simple_compat_test',
  srcs = [
    'src/simple_compat_test.cc',
  ],
  deps = [
    ':sparsehash',
  ],
)

cxx_binary(
  name = 'simple_test',
  srcs = [
    'src/simple_test.cc',
  ],
  deps = [
    ':sparsehash',
  ],
)
