VERSION_H = """
#ifndef sodium_version_H
#define sodium_version_H

#include \\"export.h\\"

#define SODIUM_VERSION_STRING \\"1.0.11\\"

#define SODIUM_LIBRARY_VERSION_MAJOR 9
#define SODIUM_LIBRARY_VERSION_MINOR 3


#ifdef __cplusplus
extern \\"C\\" {
#endif

SODIUM_EXPORT
const char *sodium_version_string(void);

SODIUM_EXPORT
int         sodium_library_version_major(void);

SODIUM_EXPORT
int         sodium_library_version_minor(void);

SODIUM_EXPORT
int         sodium_library_minimal(void);

#ifdef __cplusplus
}
#endif

#endif
"""

def merge_dicts(x, y):
  z = x.copy()
  z.update(y)
  return z

genrule(
  name = 'version.h',
  out = 'version.h',
  cmd = 'echo "' + VERSION_H + '" > $OUT ',
)

cxx_library(
  name = 'libsodium',
  header_namespace = '',
  exported_headers = merge_dicts({
    'version.h': ':version.h',
  },
  subdir_glob([
    ('src/libsodium/include/sodium', '*.h'),
    ('src/libsodium/include', '*.h'),
  ])),
  headers = subdir_glob([
    ('src/libsodium/include/sodium', 'private/*.h'),
  ]),
  srcs = glob([
    'src/libsodium/**/*.c',
  ]),
  visibility = [
    'PUBLIC',
  ],
)
