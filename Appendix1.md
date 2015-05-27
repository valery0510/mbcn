# 附录1 交易脚本的操作符、常量和符号

表A-1列出了将脚本压入堆栈的操作符。

**表A-1 入栈操作**

| 关键字 |值（十六进制）| 描述 |
| -- | -- | -- |
| OP_0 or OP_FALSE | 0x00 | 一个字节空串被压入堆栈中 |
| 1-75 | 0x01-0x4b | 把接下来的N个字节压入堆栈中，N 的取值在 1 到 75 之间 |
| OP_PUSHDATA1 | 0x4c | 下一个脚本字节包括N，会将接下来的N个字节压入堆栈 |
| OP_PUSHDATA2 | 0x4d |下两个脚本字节包括N，会将接下来的N个字节压入堆栈 |
| OP_PUSHDATA4 | 0x4e | 下四个脚本字节包括N，会将接下来的N个字节压入堆栈 |
| OP_1NEGATE | 0x4f | 将脚本-1压入堆栈 |
| OP_RESERVED |0x50 | 终止 - 交易无效（除非在未执行的 OP_IF 语句中） |
| OP_1 or OP_TRUE | 0x51 | 将脚本1压入堆栈 |
| OP_2 to OP_16 | 0x52 | 将脚本N压入堆栈，例如 OP_2 压入脚本“2” |

表A-2列出了有条件的流量控制的操作符。

**表A-2 有条件的流量控制操作**

| 关键字 | 值（十六进制） | 描述 |
| -- | -- | -- |
|OP_NOP | 0x61 | 无操作 |
| OP_VER | 0x62 | 终止 - 交易无效（除非在未执行的 OP_IF 语句中） |
| OP_I | 0x63 |如果栈项元素值为0，语句将被执行 |
| OP_NOTIF | 0x64 | 如果栈项元素值不为0，语句将被执行 |
| OP_VERIF | 0x65 | 终止 - 交易无效 |
| OP_VERNOTIF | 0x66 |终止 - 交易无效 |
| OP_ELSE | 0x67 | 如果前述的OP_IF或OP_NOTIF或OP_ELSE未被执行，这些语句就会被执行 |
| OP_ENDIF |0x68 | 终止 OP_IF, OP_NOTIF, OP_ELSE 区块 |
| OP_VERIFY| 0x69 | 如果栈项元素值非真，则标记交易无效 |
| OP_RETURN | 0x6a | 标记交易无效 |

表A-3列出了控制堆栈的操作符。

**表A-3 堆栈操作**

| 关键字 | 值（十六进制） | 描述 |
| -- | -- | -- |
| OP_TOALTSTACK | 0x6b | 从主堆栈中取出元素，推入辅堆栈。 |
| OP_FROMALTSTACK | 0x6c | 从辅堆栈中取出元素，推入主堆栈 |
| OP_2DROP  | 0x6d | 删除栈顶两个元素 |
| OP_2DUP  | 0x6e | 复制栈顶两个元素 |
| OP_3DUP  | 0x6f| 复制栈顶三个元素 |
|OP_2OVER  |0x70 |把栈底的第三、第四个元素拷贝到栈顶 |
| OP_2ROT  | 0x71 | 移动第五、第六元素到栈顶 |
| OP_2SWAP  | 0x72 | 如果栈项元素值不为0，复制该元素值 |
| OP_IFDUP  | 0x73 | 如果栈项元素值不为0，复制该元素值 |
| OP_DEPTH  | 0x74 | 把堆栈元素的个数压入堆栈 |
| OP_DROP  | 0x75 | 删除栈顶元素 |
| OP_DUP  | 0x76 | 复制栈顶元素|
| OP_NIP  | 0x77 | 删除栈顶的下一个元素 |
| OP_OVER  | 0x78 | 复制栈顶的下一个元素到栈顶 |
| OP_PICK  | 0x79 | 把堆栈的第n个元素拷贝到栈顶 |
| OP_ROLL  | 0x7a |把堆栈的第n个元素移动到栈顶|
| OP_ROT | 0x7b | 翻转栈顶的三个元素 |
| OP_SWAP | 0x7c | 栈顶的三个元素交换 |
| OP_TUCK  | 0x7d | 拷贝栈顶元素并插入到栈顶第二个元素之后 |

表A-4列出了字符串操作符。

**表A-4 字符串接操作**

| 关键字 | 值（十六进制） | 描述 |
| -- | -- | -- |
| OP_CAT| 0x7e | 连接两个字符串，已禁用 |
| OP_SUBSTR | 0x7f | 返回字符串的一部分，已禁用 |
| OP_LEFT | 0x80 | 在一个字符串中保留左边指定长度的子串，已禁用 |
| OP_RIGHT | 0x81 | 在一个字符串中保留右边指定长度的子串，已禁用 |
| OP_SIZE  | 0x82 |  把栈顶元素的字符串长度压入堆栈 |


表A-5列出了二进制算术和布尔逻辑运算符演示。

**表A-5 二进制算术和条件**

| 关键字 | 值（十六进制） | 描述 |
| -- | -- | -- |
| OP_INVERT | 0x83 | 所有输入的位取反，已禁用 |
| OP_AND | 0x84 | 对输入的所有位进行布尔与运算，已禁用 |
| OP_OR| 0x85  | 对输入的每一位进行布尔或运算，已禁用 |
| OP_XOR | 0x86  | 对输入的每一位进行布尔异或运算，已禁用 |
| OP_EQUAL|  0x87   | 如果输入的两个数相等，返回1，否则返回0 |
| OP_EQUALVERIFY | 0x88  | 与OP_EQUAL一样，如结果为0，之后运行OP_VERIFY  |
|OP_RESERVED1 | 0x89 | 终止 - 无效交易（除非在未执行的OP_IF语句中） |
| OP_RESERVED2 |0x8a | 终止-无效交易（除非在未执行的OP_IF语句中） |

表A-6列出了数值(算法)操作符。

**表A-6 数值操作**

| 关键字 | 值（十六进制） | 描述 |
| -- | -- | -- |
| OP_1ADD  | 0x8b | 输入值加1  |
| OP_1SUB | 0x8c | 输入值减1 |
| OP_2MUL  |0x8d | 无效（输入值乘2） |
| OP_2DIV  | 0x8e | 无效 （输入值除2） |
| OP_NEGATE | 0x8f |输入值符号取反 |
| OP_ABS  | 0x90 |  输入值符号取正 |
| OP_NOT  | 0x91 | 如果输入值为0或1，则输出1或0；否则输出0  |
| OP_0NOTEQUAL  | 0x92 | 输入值为0输出0；否则输出1  |
| OP_ADD  | 0x93 | 输出输入两项之和 |
| OP_SUB  | 0x94 | 输出输入（第二项减去第一项）之差 |
| OP_MUL  | 0x95 | 禁用（输出输入两项的积） |
| OP_DIV  | 0x96 | 禁用（输出用第二项除以第一项的倍数） |
| OP_MOD  |0x97 |  禁用（输出用第二项除以第一项得到的余数） |
| OP_LSHIFT  | 0x98 | 禁用（左移第二项，移动位数为第一项的字节数） |
| OP_RSHIFT  | 0x99 | 禁用（右移第二项，移动位数为第一项的字节数） |
| OP_BOOLAND  | 0x9a | 两项都不会为0，输出1，否则输出0  |
| OP_BOOLOR | 0x9b | 两项有一个不为0，输出1，否则输出0 |
|OP_NUMEQUAL  | 0x9c | 两项相等则输出1，否则输出为0  |
| OP_NUMEQUALVERIFY | 0x9d | 和 NUMEQUAL 相同，如结果为0运行OP_VERIFY |
| OP_NUMNOTEQUAL  | 0x9e | 如果栈顶两项不是相等数的话，则输出1  |
| OP_LESSTHAN  |0x9f | 如果第二项小于栈顶项，则输出1  |
| OP_GREATERTHAN | 0xa0 | 如果第二项大于栈顶项，则输出1  |
| OP_LESSTHANOREQUAL |0xa1 | 如果第二项小于或等于第一项，则输出1 |
| OP_GREATERTHANOREQUAL | 0xa2 | 如果第二项大于或等于第一项，则输出1 |
| OP_MIN | 1:26 |  输出栈顶两项中较小的一项 |
| OP_MAX | 1:27 | 输出栈顶两项中较大的一项 |
| OP_WITHIN | 1:28 | 如果第三项的数值介于前两项之间，则输出1 |

表A-7列出了加密函数操作符。

**表A-7 加密和散列操作**

| 关键字 | 值（十六进制） | 描述 |
| -- | -- | -- |
| OP_RIPEMD160 | 0xa6 |  返回栈顶项的 RIPEMD160 哈希值|
| OP_SHA1 | 0xa7  | 返回栈顶项 SHA1 哈希值
 |
| OP_SHA256 | 0xa8 |返回栈顶项 SHA256 哈希值 |
| OP_HASH160 | 0xa9 | 栈顶项进行两次HASH，先用SHA-256，再用RIPEMD-160 |
| OP_HASH256 |  0xaa |栈顶项用SHA-256算法HASH两次 |
|OP_CODESEPARATOR | 0xab | 标记已进行签名验证的数据|
| OP_CHECKSIG | 0xac |交易所用的签名必须是哈希值和公钥的有效签名，如果为真，则返回1|
| OP_CHECKSIGVERIFY | 0xad |  与CHECKSIG一样，但之后运行OP_VERIFY |
| OP_VERIFY | 0xae |对于每对签名和公钥运行CHECKSIG。所有的签名要与公钥匹配。因为存在BUG，一个未使用的外部值会从堆栈中删除。 |
| OP_CHECKMULTISIGVERIFY  | 0xaf |与 CHECKMULTISIG 一样，但之后运行OP_VERIFY |

表A-8列出了非操作符。

**表A-8 非操作**

| 关键字 | 值（十六进制） | 描述 |
| -- | -- |
| OP_NOP1-OP_NOP10 |  0xb0-0xb9  | 无操作 忽略|

表A-9保留关键字，仅供内部脚本调试。

**表A-9 仅供内部使用的保留关键字**

| 关键字 | 值（十六进制） | 描述 |
| -- | -- | -- |
| OP_SMALLDATA | 0xf9 |代表小数据域 |
| OP_SMALLINTEGER |0xfa | 代表小整数数据域 |
| OP_PUBKEYS |  0xfb | 代表公钥域 |
| OP_PUBKEYHASH | 0xfd | 代表公钥哈希域|
| OP_PUBKEY | 0xfe | 代表公钥域 |
| OP_INVALIDOPCODE | 0xff | 代表当前未指定的操作码 |