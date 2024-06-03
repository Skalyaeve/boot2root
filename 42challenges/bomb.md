# bomb

We reverse the `bomb` executable via [dogbolt](https://dogbolt.org/), then we clean/rework the source code:

<details><summary>show</summary>

```c
#include <defs.h>

int main(int argc, const char **argv, const char **envp);
int phase_1(_BYTE *a1);
int phase_2(char *s);
int phase_3(char *s);
int func4(int a1);
int phase_4(char *s);
int phase_5(_BYTE *a1);
int phase_6(char *s);
int fun7(_DWORD *a1, int a2);
void secret_phase();
void sig_handler(int a1);
void invalid_phase(const char *a1);
int read_six_numbers(char *s, int a2);
int string_length(_BYTE *a1);
int strings_not_equal(_BYTE *a1, _BYTE *a2);
int open_clientfd(char *name, __int16 a2);
__sighandler_t initialize_bomb();
int blank_line(_BYTE *a1);
char *skip();
int read_line();
int send_msg(int a1);
void explode_bomb();
void phase_defused();

int bomb_id = 0;
char lab_id[8] = "generic";
_BYTE array_123[16] = { 105, 115, 114, 118, 101, 97, 119, 104, 111,
                        98, 112, 110, 117, 116, 102, 103 };
_UNKNOWN node1;
_DWORD n1[8] = { 36, 134525716, 134525704, 0, 0, 0, 0, 0 };
int num_input_strings = 0;
_UNKNOWN force_to_data_0;
int _CTOR_LIST__ = -1;
FILE *stdout;
int _ctype_b;
int stdin;
_UNKNOWN object_11;
_IO_FILE *infile;
char byte_804B67F[];
char input_strings[240];
char s[1360];
char scratch[80];

int main(int argc, const char **argv, const char **envp)
{
  _BYTE *line;
  char *v4;
  char *v5;
  char *v6;
  _BYTE *v7;
  char *v8;

  if ( argc == 1 )
  {
    infile = (_IO_FILE *)stdin;
  }
  else
  {
    if ( argc != 2 )
    {
      printf("Usage: %s [<input_file>]\n", *argv);
      exit(8);
    }
    infile = fopen(argv[1], "r");
    if ( !infile )
    {
      printf("%s: Error: Couldn't open %s\n", *argv, argv[1]);
      exit(8);
    }
  }
  initialize_bomb();
  printf("Welcome this is my little bomb !!!!"
         " You have 6 stages with\n");
  printf("only one life good luck !! Have a nice day!\n");
  line = (_BYTE *)read_line();
  phase_1(line);
  phase_defused();
  printf("Phase 1 defused. How about the next one?\n");
  v4 = (char *)read_line();
  phase_2(v4);
  phase_defused();
  printf("That's number 2.  Keep going!\n");
  v5 = (char *)read_line();
  phase_3(v5);
  phase_defused();
  printf("Halfway there!\n");
  v6 = (char *)read_line();
  phase_4(v6);
  phase_defused();
  printf("So you got that one.  Try this one.\n");
  v7 = (_BYTE *)read_line();
  phase_5(v7);
  phase_defused();
  printf("Good work!  On to the next...\n");
  v8 = (char *)read_line();
  phase_6(v8);
  phase_defused();
  return 0;
}

int phase_1(_BYTE *a1)
{
  int result;

  result = strings_not_equal(a1, "Public speaking is very easy.");
  if ( result )
    explode_bomb();
  return result;
}

int phase_2(char *s)
{
  int i;
  int result;
  int v3[6];

  read_six_numbers(s, (int)v3);
  if ( v3[0] != 1 )
    explode_bomb();
  for ( i = 1; i <= 5; ++i )
  {
    result = v3[i - 1] * (i + 1);
    if ( v3[i] != result )
      explode_bomb();
  }
  return result;
}

int phase_3(char *s)
{
  int result;
  char v2;
  int v3;
  char v4;
  int v5;

  if ( sscanf(s, "%d %c %d", &v3, &v4, &v5) <= 2 )
    explode_bomb();
  result = v3;
  switch ( v3 )
  {
    case 0:
      v2 = 113;
      if ( v5 != 777 )
        explode_bomb();
      return result;
    case 1:
      v2 = 98;
      if ( v5 != 214 )
        explode_bomb();
      return result;
    case 2:
      v2 = 98;
      if ( v5 != 755 )
        explode_bomb();
      return result;
    case 3:
      v2 = 107;
      if ( v5 != 251 )
        explode_bomb();
      return result;
    case 4:
      v2 = 111;
      if ( v5 != 160 )
        explode_bomb();
      return result;
    case 5:
      v2 = 116;
      if ( v5 != 458 )
        explode_bomb();
      return result;
    case 6:
      v2 = 118;
      if ( v5 != 780 )
        explode_bomb();
      return result;
    case 7:
      v2 = 98;
      if ( v5 != 524 )
        explode_bomb();
      return result;
    default:
      explode_bomb();
  }
  if ( v2 != v4 )
    explode_bomb();
  return result;
}

int func4(int a1)
{
  int v1;

  if ( a1 <= 1 )
    return 1;
  v1 = func4(a1 - 1);
  return v1 + func4(a1 - 2);
}

int phase_4(char *s)
{
  int result;
  int v2;

  if ( sscanf(s, "%d", &v2) != 1 || v2 <= 0 )
    explode_bomb();
  result = func4(v2);
  if ( result != 55 )
    explode_bomb();
  return result;
}

int phase_5(_BYTE *a1)
{
  int i;
  int result;
  char v3[8];

  if ( string_length(a1) != 6 )
    explode_bomb();
  for ( i = 0; i <= 5; ++i )
    v3[i] = array_123[a1[i] & 0xF];
  v3[6] = 0;
  result = strings_not_equal(v3, "giants");
  if ( result )
    explode_bomb();
  return result;
}

int phase_6(char *s)
{
  int i;
  int j;
  int k;
  _DWORD *v4;
  int m;
  int v6;
  int n;
  int v8;
  int v9;
  int ii;
  int result;
  int v12;
  int v13[6];
  int v14[6];

  read_six_numbers(s, (int)v14);
  for ( i = 0; i <= 5; ++i )
  {
    if ( (unsigned int)(v14[i] - 1) > 5 )
      explode_bomb();
    for ( j = i + 1; j <= 5; ++j )
    {
      if ( v14[i] == v14[j] )
        explode_bomb();
    }
  }
  for ( k = 0; k <= 5; ++k )
  {
    v4 = &node1;
    for ( m = 1; m < v14[k]; ++m )
      v4 = (_DWORD *)v4[2];
    v13[k] = (int)v4;
  }
  v6 = v13[0];
  v12 = v13[0];
  for ( n = 1; n <= 5; ++n )
  {
    v8 = v13[n];
    *(_DWORD *)(v6 + 8) = v8;
    v6 = v8;
  }
  *(_DWORD *)(v8 + 8) = 0;
  v9 = v12;
  for ( ii = 0; ii <= 4; ++ii )
  {
    result = *(_DWORD *)v9;
    if ( *(_DWORD *)v9 < **(_DWORD **)(v9 + 8) )
      explode_bomb();
    v9 = *(_DWORD *)(v9 + 8);
  }
  return result;
}

int fun7(_DWORD *a1, int a2)
{
  if ( !a1 )
    return -1;
  if ( a2 < *a1 )
    return 2 * fun7(a1[1], a2);
  if ( a2 == *a1 )
    return 0;
  return 2 * fun7(a1[2], a2) + 1;
}

void secret_phase()
{
  const char *line;
  int v1;

  line = (const char *)read_line();
  v1 = __strtol_internal(line, 0, 10, 0);
  if ( (unsigned int)(v1 - 1) > 0x3E8 )
    explode_bomb();
  if ( fun7(n1, v1) != 7 )
    explode_bomb();
  printf("Wow! You've defused the secret stage!\n");
  phase_defused();
}

void sig_handler(int a1)
{
  printf("So you think you can stop the bomb with ctrl-c, do you?\n");
  sleep(3u);
  printf("Well...");
  fflush(stdout);
  sleep(1u);
  printf("OK. :-)\n");
  exit(16);
}

void invalid_phase(const char *a1)
{
  printf("Invalid phase%s\n", a1);
  exit(8);
}

int read_six_numbers(char *s, int a2)
{
  int result;

  result = sscanf(s, "%d %d %d %d %d %d", a2, a2 + 4,
                  a2 + 8, a2 + 12, a2 + 16, a2 + 20);
  if ( result <= 5 )
    explode_bomb();
  return result;
}

int string_length(_BYTE *a1)
{
  _BYTE *v1;
  int result;

  v1 = a1;
  for ( result = 0; *v1; ++result )
    ++v1;
  return result;
}

int strings_not_equal(_BYTE *a1, _BYTE *a2)
{
  int v2;
  _BYTE *v4;
  _BYTE *v5;

  v2 = string_length(a1);
  if ( v2 != string_length(a2) )
    return 1;
  v4 = a1;
  v5 = a2;
  if ( *a1 )
  {
    while ( *v4 == *v5 )
    {
      ++v4;
      ++v5;
      if ( !*v4 )
        return 0;
    }
    return 1;
  }
  return 0;
}

int open_clientfd(char *name, __int16 a2)
{
  int v2;
  struct hostent *v3;
  struct sockaddr s;

  v2 = socket(2, 1, 0);
  if ( v2 < 0 )
  {
    printf("Bad host (1).\n");
    exit(8);
  }
  v3 = gethostbyname(name);
  if ( !v3 )
  {
    printf("Bad host (2).\n");
    exit(8);
  }
  bzero(&s, 0x10u);
  s.sa_family = 2;
  bcopy(*(const void **)v3->h_addr_list, &s.sa_data[2], v3->h_length);
  *(_WORD *)s.sa_data = __ROR2__(a2, 8);
  if ( connect(v2, &s, 0x10u) < 0 )
  {
    printf("Bad host (3).\n");
    exit(8);
  }
  return v2;
}

__sighandler_t initialize_bomb()
{
  return signal(2, (__sighandler_t)sig_handler);
}

int blank_line(_BYTE *a1)
{
  _BYTE *v1;
  int v2;

  v1 = a1;
  if ( !*a1 )
    return 1;
  while ( 1 )
  {
    v2 = (char)*v1++;
    if ( (*(_BYTE *)(_ctype_b + 2 * v2 + 1) & 0x20) == 0 )
      break;
    if ( !*v1 )
      return 1;
  }
  return 0;
}

char *skip()
{
  char *v0;
  char *v1;

  do
  {
    v0 = fgets((char *)(80 * num_input_strings + 134526592),
               80, infile);
    v1 = v0;
  }
  while ( v0 && blank_line(v0) );
  return v1;
}

int read_line()
{
  unsigned int v0;
  unsigned int v1;
  int v2;
  int result;

  if ( !skip() )
  {
    if ( infile == (_IO_FILE *)stdin )
      goto LABEL_6;
    if ( getenv("GRADE_BOMB") )
      exit(0);
    infile = (_IO_FILE *)stdin;
    if ( !skip() )
    {
LABEL_6:
      printf("Error: Premature EOF on stdin\n");
      explode_bomb();
    }
  }
  v0 = strlen(&input_strings[80 * num_input_strings]) + 1;
  v1 = v0 - 1;
  if ( v0 == 80 )
  {
    printf("Error: Input line too long\n");
    explode_bomb();
  }
  v2 = 80 * num_input_strings;
  byte_804B67F[v1 + v2] = 0;
  result = v2 + 134526592;
  ++num_input_strings;
  return result;
}

int send_msg(int a1)
{
  int v1;
  FILE *v2;
  FILE *v3;
  const char *v4;
  const char *v5;
  int v6;
  int v7;
  int result;
  char dest[80];

  v1 = dup(0);
  if ( v1 == -1 )
  {
    printf("ERROR: dup(0) error\n");
    exit(8);
  }
  if ( close(0) == -1 )
  {
    printf("ERROR: close error\n");
    exit(8);
  }
  v2 = tmpfile();
  v3 = v2;
  if ( !v2 )
  {
    printf("ERROR: tmpfile error\n");
    exit(8);
  }
  fprintf(v2, "Subject: Bomb notification\n");
  fprintf(v3, "\n");
  v4 = (const char *)cuserid(0);
  if ( v4 )
    strcpy(dest, v4);
  else
    strcpy(dest, "nobody");
  v5 = "exploded";
  if ( a1 )
    v5 = "defused";
  fprintf(v3, "bomb-header:%s:%d:%s:%s:%d\n", lab_id,
          bomb_id, dest, v5, num_input_strings);
  v6 = 0;
  if ( num_input_strings > 0 )
  {
    do
    {
      v7 = v6 + 1;
      fprintf(v3, "bomb-string:%s:%d:%s:%d:%s\n", lab_id, bomb_id,
              dest, v6 + 1, (const char *)(80 * v6 + 134526592));
      v6 = v7;
    }
    while ( v7 < num_input_strings );
  }
  rewind(v3);
  sprintf(scratch, "%s %s@%s", "/usr/sbin/sendmail -bm",
          "bomb", "bluegill.cmcl.cs.cmu.edu");
  if ( system(scratch) )
  {
    printf("ERROR: notification error\n");
    exit(8);
  }
  if ( fclose(v3) )
  {
    printf("ERROR: fclose(tmp) error\n");
    exit(8);
  }
  if ( dup(v1) )
  {
    printf("ERROR: dup(tmpstdin) error\n");
    exit(8);
  }
  result = close(v1);
  if ( result )
  {
    printf("ERROR: close(tmpstdin)\n");
    exit(8);
  }
  return result;
}

void explode_bomb()
{
  printf("\nBOOM!!!\n");
  printf("The bomb has blown up.\n");
  exit(8);
}

void phase_defused()
{
  char v0;
  char v1[80];

  if ( num_input_strings == 6 )
  {
    if ( sscanf(s, "%d %s", &v0, v1) == 2
        && !strings_not_equal(v1, "austinpowers") )
    {
      printf("Curses, you've found the secret phase!\n");
      printf("But finding it and solving it are quite different...\n");
      secret_phase();
    }
    printf("Congratulations! You've defused the bomb!\n");
  }
}
```
</details>

So we got to find the password for each phase

## Phase 1

```c
int phase_1(_BYTE *a1)
{
  int result;

  result = strings_not_equal(a1, "Public speaking is very easy.");
  if ( result )
    explode_bomb();
  return result;
}
```

```c
int strings_not_equal(_BYTE *a1, _BYTE *a2)
{
  int v2;
  _BYTE *v4;
  _BYTE *v5;

  v2 = string_length(a1);
  if ( v2 != string_length(a2) )
    return 1;
  v4 = a1;
  v5 = a2;
  if ( *a1 )
  {
    while ( *v4 == *v5 )
    {
      ++v4;
      ++v5;
      if ( !*v4 )
        return 0;
    }
    return 1;
  }
  return 0;
}
```

```c

int string_length(_BYTE *a1)
{
  _BYTE *v1;
  int result;

  v1 = a1;
  for ( result = 0; *v1; ++result )
    ++v1;
  return result;
}
```
> Public speaking is very easy.

## Phase 2

```c
int phase_2(char *s)
{
  int i;
  int result;
  int v3[6];

  read_six_numbers(s, (int)v3);
  if ( v3[0] != 1 )
    explode_bomb();
  for ( i = 1; i <= 5; ++i )
  {
    result = v3[i - 1] * (i + 1);
    if ( v3[i] != result )
      explode_bomb();
  }
  return result;
}
```

```c
int read_six_numbers(char *s, int a2)
{
  int result;

  result = sscanf(s, "%d %d %d %d %d %d", a2, a2 + 4,
                  a2 + 8, a2 + 12, a2 + 16, a2 + 20);
  if ( result <= 5 )
    explode_bomb();
  return result;
}
```
> 1 2 6 24 120 720

## Phase 3

```c
int phase_3(char *s)
{
  int result;
  char v2;
  int v3;
  char v4;
  int v5;

  if ( sscanf(s, "%d %c %d", &v3, &v4, &v5) <= 2 )
    explode_bomb();
  result = v3;
  switch ( v3 )
  {
    case 0:
      v2 = 113;
      if ( v5 != 777 )
        explode_bomb();
      return result;
    case 1:
      v2 = 98;
      if ( v5 != 214 )
        explode_bomb();
      return result;
    case 2:
      v2 = 98;
      if ( v5 != 755 )
        explode_bomb();
      return result;
    case 3:
      v2 = 107;
      if ( v5 != 251 )
        explode_bomb();
      return result;
    case 4:
      v2 = 111;
      if ( v5 != 160 )
        explode_bomb();
      return result;
    case 5:
      v2 = 116;
      if ( v5 != 458 )
        explode_bomb();
      return result;
    case 6:
      v2 = 118;
      if ( v5 != 780 )
        explode_bomb();
      return result;
    case 7:
      v2 = 98;
      if ( v5 != 524 )
        explode_bomb();
      return result;
    default:
      explode_bomb();
  }
  if ( v2 != v4 )
    explode_bomb();
  return result;
}
```
> 0 q 777

## Phase 4

```c
int phase_4(char *s)
{
  int result;
  int v2;

  if ( sscanf(s, "%d", &v2) != 1 || v2 <= 0 )
    explode_bomb();
  result = func4(v2);
  if ( result != 55 )
    explode_bomb();
  return result;
}
```

```c
int func4(int a1)
{
  int v1;

  if ( a1 <= 1 )
    return 1;
  v1 = func4(a1 - 1);
  return v1 + func4(a1 - 2);
}
```
> 9
>
> 9 austinpowers (to unlock secret phase)

## Phase 5

```c
int phase_5(_BYTE *a1)
{
  int i;
  int result;
  char v3[8];

  if ( string_length(a1) != 6 )
    explode_bomb();
  for ( i = 0; i <= 5; ++i )
    v3[i] = array_123[a1[i] & 0xF];
  v3[6] = 0;
  result = strings_not_equal(v3, "giants");
  if ( result )
    explode_bomb();
  return result;
}
```

```c
int strings_not_equal(_BYTE *a1, _BYTE *a2)
{
  int v2;
  _BYTE *v4;
  _BYTE *v5;

  v2 = string_length(a1);
  if ( v2 != string_length(a2) )
    return 1;
  v4 = a1;
  v5 = a2;
  if ( *a1 )
  {
    while ( *v4 == *v5 )
    {
      ++v4;
      ++v5;
      if ( !*v4 )
        return 0;
    }
    return 1;
  }
  return 0;
}
```

```c
int string_length(_BYTE *a1)
{
  _BYTE *v1;
  int result;

  v1 = a1;
  for ( result = 0; *v1; ++result )
    ++v1;
  return result;
}
```
> opekmq

## Phase 6

```c
int phase_6(char *s)
{
  int i;
  int j;
  int k;
  _DWORD *v4;
  int m;
  int v6;
  int n;
  int v8;
  int v9;
  int ii;
  int result;
  int v12;
  int v13[6];
  int v14[6];

  read_six_numbers(s, (int)v14);
  for ( i = 0; i <= 5; ++i )
  {
    if ( (unsigned int)(v14[i] - 1) > 5 )
      explode_bomb();
    for ( j = i + 1; j <= 5; ++j )
    {
      if ( v14[i] == v14[j] )
        explode_bomb();
    }
  }
  for ( k = 0; k <= 5; ++k )
  {
    v4 = &node1;
    for ( m = 1; m < v14[k]; ++m )
      v4 = (_DWORD *)v4[2];
    v13[k] = (int)v4;
  }
  v6 = v13[0];
  v12 = v13[0];
  for ( n = 1; n <= 5; ++n )
  {
    v8 = v13[n];
    *(_DWORD *)(v6 + 8) = v8;
    v6 = v8;
  }
  *(_DWORD *)(v8 + 8) = 0;
  v9 = v12;
  for ( ii = 0; ii <= 4; ++ii )
  {
    result = *(_DWORD *)v9;
    if ( *(_DWORD *)v9 < **(_DWORD **)(v9 + 8) )
      explode_bomb();
    v9 = *(_DWORD *)(v9 + 8);
  }
  return result;
}
```

```c
int read_six_numbers(char *s, int a2)
{
  int result;

  result = sscanf(s, "%d %d %d %d %d %d", a2, a2 + 4,
                  a2 + 8, a2 + 12, a2 + 16, a2 + 20);
  if ( result <= 5 )
    explode_bomb();
  return result;
}
```
> 4 2 6 3 1 5

## Secret Phase

```c
void secret_phase()
{
  const char *line;
  int v1;

  line = (const char *)read_line();
  v1 = __strtol_internal(line, 0, 10, 0);
  if ( (unsigned int)(v1 - 1) > 0x3E8 )
    explode_bomb();
  if ( fun7(n1, v1) != 7 )
    explode_bomb();
  printf("Wow! You've defused the secret stage!\n");
  phase_defused();
}
```

```c
int fun7(_DWORD *a1, int a2)
{
  if ( !a1 )
    return -1;
  if ( a2 < *a1 )
    return 2 * fun7(a1[1], a2);
  if ( a2 == *a1 )
    return 0;
  return 2 * fun7(a1[2], a2) + 1;
}
```
> 1001

[laurie](../3-post-exploitation/laurie.md)'s README said:
```
Diffuse this bomb!
When you have all the password use it as "thor" user with ssh.

HINT:
P
 2
 b

o
4

NO SPACE IN THE PASSWORD (password is case sensitive).
```

- `Publicspeakingisveryeasy.126241207201b2149austinpowersopekmq4263151001` doesn't work

- `Publicspeakingisveryeasy.126241207201b2149opekmq4263151001` doesn't work

- `Publicspeakingisveryeasy.126241207201b2149austinpowersopekmq426315` doesn't work

- `Publicspeakingisveryeasy.126241207201b2149opekmq426315` doesn't work

There must be a last step to find the password

- `1001` is a valid binary number, his decimal value is `9`, which is the password for phase 4, we might need to play with binary representation of the password

- The binary representation of the last password `426315` is `1101000000101001011`, if we take the `9` last bits of it and shift them to the left, we get `1101000000010010111` which is `426135` in decimal

- `Publicspeakingisveryeasy.126241207201b2149opekmq426135` works

## Credentials found

### SSH

| Login | Password |
|-|-|
| `thor` | [Plain] `Publicspeakingisveryeasy.126241207201b2149opekmq426135` |