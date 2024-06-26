

#### 关于JVM和Class加载

- [深入理解JVM-Class文件结构和类加载 - 简书 (jianshu.com)](https://www.jianshu.com/p/88a34f2959e0)

#### JVM相关资料:

- 《深入理解jvm虚拟机》

#### 全栈知识体系:

- [| Java 全栈知识体系 (pdai.tech)](https://pdai.tech/)

-  https://bugstack.cn/

#### Integer自动装箱

- ![image-20221127111020347](https://raw.githubusercontent.com/1v10/Photo/main/photo/202211271216046.png)

- Integer的自动装箱在将int值赋给Integer时会自动变为Integer类
- 此时如果int值范围在[-128~127]会指向同一个对象,原理为Integer会缓存该范围的取值对象,在该范围则指向同一个对象

#### 正常New对象不会受到改缓存机制影响

- ![image-20221127121504547](https://raw.githubusercontent.com/1v10/Photo/main/photo/202211271215587.png)

 



#### Eclipse快捷键

- 查看继承体系:ctrl+t

- 展示当前类的目录并所可搜索:ctrl+o 仅限项目文件
- 搜索文件:ctrl+shift+r
- 全局搜索文本:ctrl+h
- Alt+left/right 进入方法后返回或者再次返回快捷键
- 搜索所有类,包括api

 

#### 泛型:广泛的类型  可变的类型

- [【Java】泛型详解（一篇就够了） - 至安 - 博客园(cnblogs.com)](https://www.cnblogs.com/birdy-silhouette/p/14743132.html)

- 关于ArrayList与LinkedList效率对比
  
  - [逼着面试官问了我ArrayList和LinkedList的区别，他对我彻底服了 - 腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/news/700913)

#### 关于集合有序的定义

- ##### [Java集合中有序无序的概念 - 简书 (jianshu.com)](https://www.jianshu.com/p/2a12630e05d6)

- ##### 集合输入输出顺序一致 即为有序 

- ##### 有序便代表具有可预测的迭代顺序

- ##### 关于ArrayList和 linkedList插入速度

  - [面经手册 ·       第8篇《LinkedList插入速度比ArrayList快？你确定吗？》 | bugstack 虫洞栈](https://bugstack.cn/md/java/interview/2020-08-30-面经手册 · 第8篇《LinkedList插入速度比ArrayList快？你确定吗？》.html)

#### 集合

- 出现背景:数组的容量固定,当容量不足时需要重新创建数组,而集合的长度是可变的,会自动扩容,属于动态存储容器

- ##### 集合与数组的区别

  - |      | 存储类型                            | 动态性                  |
    | ---- | ----------------------------------- | ----------------------- |
    | 数组 | 基本数据,引用                       | 容量固定不可变          |
    | 集合 | 引用,可以存基本数据是因为会自动装箱 | 容量不会固定,会自动扩容 |

- ##### 迭代:集合的遍历 有些集合没有下标.不能通过下标来获取对象,所以无法使用for

  - 获取迭代器 使用迭代器 hashNext(判断是否还有下一位),next(获取下一位)

  - 迭代器可以通过集合获取,也可以再泛型类中实现迭代器接口自定义迭代器
  - 迭代器通过当前集合状态获取 不可修改集合

#### 集合的遍历方式

- List: 迭代器(通过当前集合生成),for(依赖通过下标获取元素方法),forEach(底层为迭代器)

- Set:迭代器,forEach()

- ##### 迭代器iterator注意事项

  1. 迭代器根据当前集合元素生成,所以使用迭代器遍历时不可用list修改元素,如果迭代器遍历同时修改会抛出并发修改异常,如果需要删除,可以使用迭代器本身的remove方法进行山,如果需要添加集合元素,需要使用list迭代器(Listiterator)的特有add方法进行
  2. 如果使用contains()判断list是否包含某引用元素,底层为对象的equals方法 ,所以需要重写        equals方法

#### Vector

- 跟ArrayList一样底层为数组实现,但是其是同步,线程安全,效率低,而ArrayList是不同步的,效率高
- LinkedList也是线程不安全

#### 数组和链表

- 数组实现随机访问快(索引),插入删除慢(因为其有序有索引,删除后元素会进行移动,插入指定位置后,两边元素也需要进行移动)
- 链表实现随机访问慢(无索引,其查找需要遍历对比),插入删除快(因为其链表只需要被删元素或者增加元素前后元素更换指向引用即可)

- 单向列表:当前值,下一个元素值
- 双向列表:前一个值,当前值,下一个元素值

#### 泛型

- 安全性:提供了编译阶段类型检查 如果不进行类型检查 统一为object 在某些条件下 对象获取转换时吧会引发类型转换异常(classCastException) 本质上是要指定参数类 由于该参数类拥有广泛范围  所以为泛型
- 便捷性:由于指定了参数类型 进行对象转换时操作较为方便
- 泛型类、泛型方法 、泛型接口

- <？ extends T > 限定了参数类型为T以及其子类    参数上限
- <?  super T> 限定了参数类型为T以及以及其父类   参数下限

#### forEach

- 底层为迭代器
- 简化数据和collection接口的便利
- for(类型 实例:集合){}

#### 关于ArrayList的删除

- for循环删除ArrayList中元素后,List元素会进行移位操作（i++）,n为当前删除元素下标,n+1的元素会自动向前移位到n位置,此时i已指向下一位置(n+1),判断获取会漏掉移位后n+1元素, 所以注意此类操作后删除后, for循环位置减1再开始判断 ,而迭代器是next手动获取后才会移位,不会自动移位！所以 迭代器和foreach不会有此问题
- ![image-20221117204235029](https://raw.githubusercontent.com/1v10/Photo/main/photo/202211271215343.png)

#### 可变参数

- 数据类型.....arr  同一类型参数数量可以变化  底层为数组

#### HashSet

- 底层为HashMap,原理为把存入元素当作k,v直接创建一个object对象模拟键值对,

- 无索引,存取顺序不一致,不容许数据重复,容许null但只容许一个
- 禁止重复是根据对比hashcode()和equals()方法进行对比的
  - 对比完hashcode值相等才会去对比equals()方法进行二次对比
  - 所以使用hashset的类需要重写hashcode()和equals()方法
- 可以进行迭代和forEach(),迭代器是conllection类定义的,其子类都会实现   
- hashcode():重写时尽量保证属性相同的生成相同的值，不同的属性生成不同的值
- equals()：重写 属性相同返回true 属性不同返回false 返回false则进行存储

#### LinkedHashSet

- 有序的HashSet 既能保证有序又能保证元素唯一

#### Treeset

- 底层为TreeMap,红黑树

- 无序,但对元素排序,可保持唯一

- 传入是会自动把元素提升为比较类型,如果自然顺序则提升为(Comparable,所以需要实现该接口),入宫使用比较器,则提升为比较器类型,如果不指定比较器,就会报类型转换异常

- 排序的方法时依赖于类的compareTo()进行排序,底层为二叉树,所以需要实现camparable接口实现compareTo()

- 排序实现方式:第一个元素为根节点,使用类compareTo()比较,比根节点大则在左侧,比根节点小则在右侧,形成一个二叉结构,

- 遍历顺序为从左到根元素再到右

- 保持唯一 根据compareTo()返回值判断的,返回0代表重复

- 在元素添加时对象会自动被提升为comparable

- ##### 比较元素.campareTo(被比较元素);存储的位置与该方法返回值有关,

  - 0:比较元素=被比较元素,不予存储
  - 1:比较元素>被比较元素,比较元素存储在被比较元素的右边
  - -1:比较元素<被比较元素,比较元素存在被比较元素的左边

- String的比较方法是按照unicode编码字符对应的数字进行比较

- ##### 比较器:创建Treeset(Comparator<比较类> c)时传入比较器

  - 使用场景:某些类型存入时比较,默认调用其compareTo()方法,该比较为自然顺序,无法自定义,所以需要使用比较器
  - 自定义比较器需要实现接口(comparator),重写compare()方法

- ##### 关于接口的多态体现

  ```
  为什么接口最能体现多态?因为接口和实现类的关系,以及各个实现类之间的关系,不像父类和子类之间,子类和其他子类之间的要求那么严格...举个例子,拿"吃饭"这个method举例...如果把这个method声明在父类中,那么子类必须要和父类是"同类",父类是人,那么"吃饭"这个功能就被限制死了,只能被人来完成...如果把这个功能声明在"接口"中,那么完成这个功能的不光能是人,可以狗,可以是猫,可以是任何东西,只要它能"吃饭"...这个就最大限度地体现了"多(种形)态"...接口的多态性,就体现在只关心"你能做什么",而不关心"你是谁"...
  链接：https://www.zhihu.com/question/48023110/answer/1101654535
  ```

  

#### Map

- 将键映射到值的对象

- 一个映射不容许重复的键

- 一个键只能对应一个值

- ##### 与Conllection体系区别:

  - Conllection是单列集合,Map是双列集合
  - Conllection的数据结构针对元素本身,而Map的数据结构针对键
  - Conllection的set元素唯一,Map的键唯一

- Map集合的遇到重复键不存入,但会更新该键所映射的值的值为重复键的值,put()方法会返回被覆盖键所映射的值 

- ##### Map遍历

  * *Map集合无法使用迭代器,因为迭代器专属于单列集合 通过一些方法获取到set集合然后使用迭代器或者foreach进行遍历
  * 获取所有值进行遍历,values(),返回所有值set集合
  * 获取所有键调用get(k)遍历,keyset() rerurn set
  * 获取所有Entry对象(包含键与值)遍历,entrySet() return set
  * Entry是map接口的内部接口,其子类获取Entry对象需要内部类实现该内部接口  implements Map.Entry<K,V>

- #### Iterator

  - 针对Collection的遍历工具 其本身不是集合 不存储元素,只是用来访问集合
  - 迭代:重复一个过程进行反馈 每次反馈的结果作用于下一次过程的初始值

  

#### HashMap

- put()过程

- ##### 关于几个名词的含义:

  - capactiy:数组容量, 初始容量默认16,必须为2的n次幂,loadFactor:负载因子(数组所能负载的程度,扩容阈值比例),threshold(扩容阈值),size:存储的元素个数
  - 负载因子越小越容易空间浪费,越大越容易hash冲突导致链表越长,所以0.75最为合适

- 底层首先创建node数组(jdk1.7为entry,功能相同),数据中每一个元素为node节点,node对象包含k,v,next值,相同的hash值会使用链表存储,数组初始长度为16,加载因子为0.75,扩容倍数为2

- 关于相同key的hash值一样,先判断原位置有无元素以及链接,如果有开始遍历进行覆盖值的操作

- 去重算法与HashSet一致,依赖元素的hashCode()和equals()方法

- 无序集合,不保证存储顺序(底层存储位置依赖的 hash算法,并非按照插入顺序存储),也不保证存储顺序是不变的(自动扩容后会重新计算元素位置)

-  底层结构:数组+链表+红黑树(jdk1.8新加入)

- 链表:为了解决hash冲突,由于hashCode值相同,所经过hash算法后的位置值相等,那么就将hash值相等的元素用链表串起来

- #### 红黑树:

  - 为了解决链表单向链表过长,导致的访问效率问题,转换阈值为8,(链表大于8且数组长度>64,会进行转换,如果<64转红黑书效率比链表低,如果数组长度<64,会首先进行扩容为32,扩容后位置重新计算,如果链表还大于8,那么再次扩容,如果还大于8就会转红黑树),如果红黑树小于6会转回链表
  - 为什么8且capacity为64才扩容,因为红黑树占用空间是链表的2倍,在<8且<64的场景下效率也不如链表,时间和空间的权衡,而且链表长度>8概率非常小

- 负载因子:数组进行扩容的临界百分比

- ##### hash算法(计算hash值,注意,此hash值不是index数组下标)

  - ##### hash算法:hash=key ^ (key.hashCode >>>16)   注意hash算法计算的值不是索引值

    - 因为最后进行运算的是低位,如果高位变化大,而低位不变也会增加hash冲突,此举不但将高位与低位进行混合增加随机性,并且异或运算后低位的特征也得到保留
    -  [hashmap的hash()原理.pdf](..\..\桌面\hashmap的hash()原理.pdf) 

  - index值(索引值):inde=hash$(n-1)，该值才为索引值,该方法的本质是为了压缩hash值

    - 为什么是n-1,注意数组长度n为偶数,n-1后为奇数,奇数最后一位为1,偶数最后一位为0,如果为偶数,那么最后1位永远为0,某些位置永远映射不到值
    - 此时hash()决定了index值,n不变,此时相同的hash值会计算出相等index,那么hash算法得出
    - hash碰撞:即计算出的hash值相等

  - ##### index相同如何处理

    - 如果index有元素,如果通过hashCode值和数组长度计算出来的index相等，那么就循环遍历(只有一个元素,链表,红黑树)调用equals方法判断key是否相等,如果key相等，那么就执行值覆盖操作,如果key不相等，继续判断,直到链表最后一位元素，挂到该元素下面,如果是红黑树,执行判断挂到相应位置

  - hashcode返回为32位int数,首先将该值高16位与低16位位运算,让数字尽可能的分散,然后且运算size-1

  - 扩容后的位置计算,hashcode值与size 且运算 为0则在原位置,不为0则(原位置+size),扩容后的该算法正好与重新计算位置的结果一致
  
  - 容许null值,null值的hash为0

#### 数据结构

- 数据存储的方式,储存存储的方式可以决定数据的运行和存储的效率

#### LinkedHashMap

- 有序的HashMap

#### TreeMap

- 其排序也是针对的key 底层为TreeMap

#### HashTable

- 实现Map接口,后被HashMap替代

- HashTable是线程安全的

- ##### 与HashMap相比

  - 相同点:Hash算法,双列集合,key唯一
  - 不同点:HashTable是线程安全的,HashMap是线程不安全的,HashTable不可以存储null键和null值

#### 泛型边界

- ? extends E   固定泛型上边界:表示E及E的子类
- ? super E  固定泛型下边界:表示E及E的父了类

#### 让整数n 经过某个算法在某个区间:例如在0-15

- random(n) 利用random随机数并限定范围
- n%16  对范围最大数取余数即可
- n & 15    
  - 15的二进制为1111,前面位数全为0,所以&任何数,后4位之前全为0,因为&运算全是1才是1,那么此时n的二进制后4位&15的二进制, 此时最大值为1111,最小为0000

#### 关于整数的取值范围:

- 取决底层的字节数n,无符号取值范围:0~2的n-1次幂,有符号, 

- 有符号取值范围: 负数 2的n-1次幂  到 2的n-1次幂-1
- 比如byte的取值范围为[-128-127],理论上是[-127-127],为什么却不是?计算机底层并非用原码表示数值,而是用补码,正数,原码,补码,反码均相同,而负数需要除符号位都取反再加1才算表达补码,-128的补码表示是10000000,通过-127+-1算出来的,本质是占了-0的表达

#### 查询时间复杂度

- 单向链表:O(n)

- 双向链表:O(n)

- 二分查找:O(log2N)

#### 	二叉树:0(h)   

- 某些情况下树的结构性可能很差,例如左边或者右边的节点深度高,成为了双向链表,某些节点的查询时间复杂度为0(n),没有了树的意义

​		![image-20221121183058755](https://raw.githubusercontent.com/1v10/Photo/main/photo/202211271215136.png)

#### 	完全平衡二叉树: 

- 左右子树的深度差不超过1,当发现左右节点深度超过1时,旋转节点更换各个顶部节点重新排列以达到平衡,缺点:所有节点完全进行旋转较为浪费时间,每次插入删除都要进行旋转,维护平衡代价较高

![image-20221121183130142](https://raw.githubusercontent.com/1v10/Photo/main/photo/202211271215291.png)

#### 红黑树:

- 是一种不完美平衡树,介于二叉树与完全平衡二叉树之间,部分平衡即可

- 将节点分为黑色和红色,只要求黑色节点高度差不为1

#### 异常:

- #### Throwable

  - Error:服务器、数据库重大错误

  - ##### Exception:编译异常、运行时异常

    - ##### RuntimeException ：运行时异常

    - 其他异常：编译异常,必须处理否则不通过编译

    - 自定义异常：针对程序所建立的定制化异常

      - 自定义异常类继承Exception 

  - ##### 异常处理机制:异常出现后会抛出异常

    - 默认处理机制:打印异常类、异常信息、异常位置

    - ##### 人为处理

      - 捕获异常后
        - try捕获异常后catch处理,代码会自动从catch以下继续执行,不会继续执行try里面的代码
        - try catch
        - try catch finally
        - try finally
          - finally 为try语句体,针对方法结束前所做操作,程序出现异常一定会执行,初步出现异常都会执行，除非jvm退出,用于释放资源,例如关闭io流
          - finalize:针对于对象被回收前 所作操作
          - final:本意为不可变 针对于类、方法、引用数据类型、基本数据类型 
          - finally与return优先级
          - return会先建立返回路径以及返回数据,然后去执行finally再返回
      - 抛出异常：程序内部不能处理，由调用者处理
        - 抛出后不会继续执行代码,如果需要继续执行必须try catch
        - throw   方法内部抛出 只能抛出一个异常
        - throws 方法声明上 可以抛出多个异常
        - 继承重写抛出异常方法时:子类抛出异常必须是父类异常或者异常子类,父类抛出多个异常,子类只能抛出其子集,子类抛出异常不能比父类多

#### IO:

- 处理设备间数据传输
- Java对数据的传输是通过流的方式
- 操作流的类都在IO包下
- 按照方向可分为:输入流、输出流
- 使用完毕需要关闭通道,如果io流写在异常处理体系内,会自动关闭,流实现AutoCloseable
- #### 关于字符编码：
  
  - 字符：各种文字、符号
  - 计算机存储数据都是二进制数字形式,而显示在屏幕是数字对应的字符
  - 解码：把二进制数解析为字符
  - 编码：把字符转为二进制数
  - 字符集：字符字典,字符所对应的二进制数,如a为97
    - ASCII
      - 美国最规定的编码及，针对英语字符、符号的字典
    - Unicode
      - 统一码,编码了世界上大部分的文字系统
      - 不同字符符号所占字节不同
  - 字符编码：由于字符集只是规定了不同字符对应的字符数字体现形式,例如a为97,将不同字符转为二进制进行表现,而字符编码就是转为二进制数的规则 字符在计算机中的二进制体现规则
  - 针对不同的字符符号使用不同大小的字节编码存储
    - 会调用码表对应规则进行编码
  
- #### File:文件类

  - 代表文件,需要传入文件路径以及文件
  - 可以判断文件是否存在、删除文件、重命名文件、创建文件以及文件夹、判断是否可读可写、判断是文件还是目录、可以判断某一文件是否在文件夹中

- ##### RandomAccessFile：随机访问流,可以任意对文件进行随机访问，包括读取和写入,整合类输入流输出流（写时可以指定索引,读时可以按照索引读取),该流可以用到多线程下载,分配多个线程下载文件的不同位置

- #### 输入流

  - ##### 节点流:可以向某个特定地方(节点)读写数据,是一个完整的流

    - ###### InputStream:InputStream：抽象类,字节输入流超类

    - ###### Reader:抽象类,字符输入流超类

    - ###### FileReader:文件字符输入流

    - ###### LineNumberReader:带有行号的字符缓冲流

    - ###### SequenceInputStream:  可以将多个输入流串联,从第一个流开始读取，然后第二个

    - ###### FileInputStream:文件字节输入流,可以读取文件,

      - 文件的末尾标记为-1，当读取到-1默认已到达文件末尾,-1为结束标记
      - read()方法每次读取一个字节,而-1的二进制补码为11111111,假如读取到的数据字节正好是-1,那么如何分辨是结束标记还是数据字节-1呢? read()方法的接收值为int，结束标记-1采用int类型,而正常读取的数据使用byte类型，当判断是byte类型数据时直接前面加24个0转为int类型从而可以接收,而write()方法写入数据时会再次把int转为byte,不会改变文件数据 
      - read()每次读取只读取一个字节效率太低,但是不一个一个读取不知道要读取多少个字节，可以通过available()方法获取剩余字节个数，read(arr)方法可以传一个数组,一次性读取该数组大小的字节个数，因为是将文件读取到内存，如果文件过大,会导致内存溢出,可以控制数组大小,定义小数组读取,定义大小为1024*n,方便理解大小

    - ObjectInputStream:

  - ##### 处理流:对一个已知流进行封装升级(在已有基础上装饰)，提升功能和效率

    - ###### BuffedInputStream：字节缓冲流

      - 底层为一个小数组,大小为8192
      - 从输入流到程序中间建立了缓冲区,将字节读取到缓冲区，再读取到程序,注意缓冲区建立在内存，提高每次交互的数据量,减少交互次数,缓冲区满才会执行写入
      - close(),关闭流,关闭流之前会一次性将缓冲区内数据写入
      - flush(),刷新缓冲区,将缓冲内数据写入,刷新完后可以继续写

    - ###### BuffedReader：字符缓冲流

      - 可以读取(写入)一行ReadLine(),利用/n 回车 来判断该行结束

      - ###### LineNumberReader:带有行号的字符缓冲流,可以设置和获取行号

    - ###### ObjectInputStream:反序列化流

  - ##### 字符流

    - 可以指定字符集进行写入读取

    - 字符首字节都是负数,字符流通过此来分辨几个字节是否表达一个字符

    - 读取字符的流

    - 只读或者只写时,使用字符流

    - 拷贝使用字节流,因为原字节的搬运,不涉及转换,而字符流会进行转换,效率较低,而且拷贝在读取非纯文本文件,有可能某些字节找不到相对应的字符,会用?号代替,而文本都有对应字节

    - 字节流读取只中文,由于中文不止一个字节,所以读取后重新组合会导致乱码,所以需要使用字符流

    - ###### Reader:抽象类,字符输入流超类

    - ###### FilerReader 文件字符输入流

    - ###### BuffedReader：字符缓冲流

    - ###### LineNumberReader:带有行号的字符缓冲流

  - ##### 字节流

    - ###### InputStream

    - ###### FileInputStream

    - ###### BuffedInputStream

    - ###### SequenceInputStream

- #### 输出流

  - ##### OuputStream:抽象类,字节输出流超类

    - ###### FileOuuputStream:文件字节输出流，

      - write(),虽然写的是int数,但会转换成byte
      - write(arr)讲数组中的字节一次性输出

    - ###### BufferedOutputStream

    - ###### SequenceOutputStream

    - ###### ByteArrayOutputStream:字节内存缓冲流,先将字节存到缓冲区（可扩容）,再一次性获取输出(QQ聊天打字)
  
  - ###### DataOutputStream:基本数据类型操作流
  
    - ###### PrintWriter:
  
    - ###### PrintStream:打印字节流
  
      - System.out便是打印流
      - 打印对象默认调用toString()
      - 打印基本类型都会转为String输出
      - 底层会将Stirng拆为char数组使用字符输出流输出
      - 可以修改输出流的目的地
  
    - ###### ObjectInputStream:对象操作流 序列化流 序列化(将对象转为字节序列) 用于存储对象和传输
  
      - 为什么不能把对象直接转成字节?  因为没有相对应的规则没办法把对象还原回来,比如把房子拆成木头,如果没有图纸规则,就没办法组装回来
      - 序列化的本质是将对象转为字节序列,并制定一种转换规则(类似于编码规则),那么存储和还原都可以使用这种规则
      - 被序列化的对象必须实现这种转换规则
      - 多个对象存到集合,序列化集合即可
      - 被序列化的对象要实现Serializable接口告知(标记)Jvm虚拟机该对象要被序列化
      - serialVersionID: 对象版本号,保证写和读时是一个对象版本(写之后可能对对象进行修改,此时对象版本号不一致)
        - 如果修改对象后(例如添加属性)不更改版本号,那么反序列化后该属性会为空
  
  - ##### Writer:抽象类,字符输出流超类
  
    - ###### FileWriter:文件字符流
    
    - ###### buffedWriter:字节缓冲流

#### Properties

- HashTable子类,双列集合,作为项目配置文件内容使用, k,v都为String

#### 递归

- 函数的定义中使用函数自身的方法
- 必须存在递归出口(递归结束的条件)

#### 多线程

- #### 线程:是程序执行的一条路径，一个进程可以含有多个线程

  - ##### 程序:指令集(代码)和数据的合集,是静态的。存在于硬盘上

  - ##### 进程：运行中的程序,程序的实例

    - ##### 线程：进程中的子任务

- #### 多线程类型

  - ##### 多线程并发:多条路径交替执行,称为多线程并发,同时出发,不必等待一个路径执行完再去执行另一个，由于交替间隔较短，所以使人感觉在同时运行

  - ##### 多线程并行:多个路径同时执行,出现在多核心CPU,一个核心处理一条路径

- #### Java程序运行原理

  - JVM程序运行成为Jvm实例(Jvm进程),Jvm进程加载.class文件,称为Java进程
  - Jvm就是多线程,例如有垃圾回收线程和主线程

- #### Thread :线程类,可以利用该类创建更多的线程

  - ##### extends Thread:重写run()方法,将要执行的新线程代码写在run()中,使用start()开启新线程

  - ##### new Thread(implements Runnable).start:实现Runnable接口,重写run(),将该类传入Thread构造,Thread有Runnable子对象,当调用Thread.run()会自动调用Runnable实现类的run()

  - ##### new Thread(new Runnable(){run()}).start():使用匿名内部类(类似局部内部类,生命周期在方法中)实现Runnable接口然后传入Thread构造，使用匿名类内部相当于实现接口或者继承父类

  - ##### new Thread(new Thread(){run()}).start():使用匿名内部类继承Thread，重写run()方法

    - 匿名内部类和局部内部类在使用局部变量时,局部变量必须为final,因为匿名内部类如果使用非final变量,可能在使用时局部变量已经消失了或改变了,利用final加入常量池延长局部变量生命周期和不可修改性

  - ##### 线程相关方法:

    - 关于为什么不run()直接开启线程,run()里面还要写代码,当执行run()方法的代码时线程还未开启,此时是单线程,失去了多线程的意义,先利用start()开启线程,等开启后便可多线程执行代码
    - 获取线程相关信息,设置、获取线程名、获取线程对象,run()方法里面的this就是当前线程对象
    - sleep()休眠线程:让当前线程休眠,暂时停止执行,一定时间后苏醒参数可以传休眠时间(毫秒)
    - wait()等待线程:让当前线程等待,无法自动停止等待,需要调用notify()让其停止等待
    - setDaemon()守护线程:设置当前线程为守护线程,该线程用于服务其他线程,如果剩余线程都为守护线程,则Jvm退出
    - join()加入线程:相当于插队,当前线程暂停,等待加入线程(调用join()的线程)执行完毕,再继续执行,如果传入暂停参数,当暂停一定时间后,继续交替执行
    - yield()礼让线程:让出执行权,让其他线程执行
    - setPriority()设置线程优先级:最小为1,最大为10,默认为5

- #### 线程安全

  - 背景：当多个线程同时运行,线程的调度由操作系统决定,任何一个线程都有可能在任何指令处被操作系统暂停,然后某个时间段再继续执行,此时如果多个线程操作同一个共享变量,就有可能导致数据不同步问题,导致线程不安全,此时需要某种措施来实现线程的同步

  - ##### 线程同步 

    - 线程同步是实现线程安全的一种手段

    - 死锁:两个或两个以上的线程,因争夺资源造成相互等待的一种状态

      - 本质原因:双方都持有对方所需要的锁,而双方又不释放所持有的锁,所以造成相互等待

    - ###### synchronized:

      - 同步代码块:使用synchronized(同步锁对象){}将代码包住,同步局部代码块,任何线程在执行含有同步锁的局部代码时,会检查当前锁对象是否被占用,如被占用,等待锁对象释放,如未占用,占用锁对象,执行同步代码,局部代码块的锁对象可以指定

      - ###### 同步方法:方法声明上加synchronized,锁对象默认为this

        - 为了符合面向对象的思维,当发送消息给对象,编译器会暗中把当前对象的引用传给方法,可以使用this调用,this便是方法调用者

      - 同步静态方法:锁对象默认为类对象(字节码对象),类名.class

      - 同步锁对象:可以是任意对象,但是注意想实现线程同步的几个线程获取的锁对象必须是同一个锁对象(同一个引用)

    - Reentrantlock:互斥锁

      - 具有与synchronized相同的一些行为和语义，该类为新同步实现类,创建对象实例使用,reentrantlock会为每个线程创建一个Condition实例(对应对象锁)
      - lock():获取锁
      - unlock():释放锁
      - await():当先线程等待
      - signal():指定唤醒,唤醒调用该方法的Condition对应线程

  - ##### 线程安全集合

    - 线程安全:Vector、Stringbuffer、Hashtable、CurrentHashMap
    
    - 线程不安全：ArrayListList、HashSet可以用Collections.synchronizedxxx()将其转化为线程安全,底层用synchronized修饰方法
    
    - concurrentHashMap
    
      - Hashtable: 性能低,操作时会将整个数组锁住
      - jdk1.7:分段锁,底层创建segment数组,将原HashMap分段,分别存入该数组,执行分段锁机制,每个分段的锁对象为segment对象,写锁读不锁
      - jdk1.8:数组+链表+红黑树的方式实现，而加锁则采用CAS和synchronized实现
        - [JUC集合: ConcurrentHashMap详解 | Java 全栈知识体系 (pdai.tech)](https://pdai.tech/md/java/thread/java-thread-x-juc-collection-ConcurrentHashMap.html)
        - [Java并发之CAS原理分析 (objcoding.com)](https://objcoding.com/2018/11/29/cas/)
        - 1.8 concurrentHashMap同步设计
          - 数据每个节点对象node都用volatile修饰,保证可见性与顺序性
          - put(),如果索引处为空,则cas插入
          - put(),如果索引处不为空,将锁住该节点体系(链表,红黑树)
          - 扩容以及,利用标志判断是否有线程在处理,标志值用volatile修饰,修改标志值用cas操作,扩容后重新添加到数组也是执行cas操作
          - get(),使用cas获取
    
      - Cas(campare and swap):unsafe类,提供了实现原子操作的的方法
        - 三个操作数:内存值(内存地址上最新的变量值,配合voliatile提供可见性),期望值(想象中将被改变的值),新值,如果内存值与期望值相同,则将期望值变为新值,否则不执行
        - 原子操作:操作过程不会被线程调度机制打断,这种操作一旦开始,就一直运行到结束,要么整个操作过程全部执行不被打断,要么就都不执行
          - 原子:化学反应中不可再分的基本微粒
        - cas只能保证原子性,不能保证可见性和有序性,需要voliatile帮助
        - Voliatile:修饰变量
          - 可以保证可见性: 线程对于变量的改动,其他线程可见
          - 有序性:禁止指令重排
          - 不保证保证原子性

  - ##### Runtime:该类为单例模式 运行时类,代表当前运行环境,里面封装了一个JVM进程

    - exec():让JVM执行命令 

  - ##### Timer:计时器 为线程安排定时任务

    - schedule(extends timertask,time):指定时间执行指定定时任务,也可重复执行,TiimeTask类实现runnable接口,拥有run()方法

  - ##### 线程通信

    - 线程执行是乱序的,而让线程之间通信,可以让线程之间拥有秩序

    - wait():让当前线程等待,且释放锁对象,该方法在哪个线程调用哪个线程等待,与调用者无关

      用哪个对象锁就用那个对象调用wait()

    - notify():唤醒在此对象监视器上等待的单个线程，唤醒等待线程,让该线程成为就绪状态,加入调度队列(交替执行队列),如果有多个等待线程，则随机唤醒一个线程，注意:线程在哪里等待,唤醒后会继续从哪里执行,不会执行之前代码

      - monitor(对象监视器)：每个对象和类都有对象监视器,来控制当前对象只有一个线程访问,当锁被占用,其他线程需要等待锁，简单来说,对象监视器实现对象锁的功能
      - [Object的对象监视器 - 掘金 (juejin.cn)](https://juejin.cn/post/6900029764514349064)
      - 与sleep区别:sleep不会释放锁,sleep必须传入参数,nofity也可以传递参数让其自动苏醒

    - notifyAll();唤醒所有等待线程

  - ##### ThreaGroup线程组类：对线程分组管理调用

    - 线程默认组为主线程组
    - 线程组信息可以调用线程对象获取
    - 线程所属组可以在线程创建时将线程组对象传进去,该线程就属于该组
    - 可以同时将一组线程设置为礼让线程,等待线程

  - ##### 线程状态:

    - 新建状态:线程正在创建
    - 就绪状态:线程加入线程调度,有执行资格,无执行权
    - 运行状态:线程正在运行,有执行资格,有执行权
    - 阻塞状态:线程不加入线程调度,无执行资格,无执行权,例如sleep(),wait(),资源获取中
    - 死亡状态:线程执行完毕,线程死亡
    - ![image-20221125213422776](https://raw.githubusercontent.com/1v10/Photo/main/photo/202211271215189.png)

  - #####  线程池

    - 提供线程的类,不必再自行创建,只需要给线程池提供任务即可,可以让线程池管理维护线程,线程池中的线程执行完后不会死亡,会空闲,等待下一个对象使用
    - Java内置线程池，ExecutorsService，该类获取设计为工厂模式,根据调用者所需对象实例来创建不同的实例,需要使用Executors线程池工厂类来获取
    - Executors.newExecutorsService(线程数量).submit(implements Runnable 所要执行的任务)
    - shutdown() 关闭线程池
    - submit(implements callable):线程池任务类也可以使用callable,实现callable,重写call方法即可,用来计算结果

#### 监听器(Listener)

- 监听事物运行状态以做出响应
- 事件源:事件产生源头,被监听的事物
- 事件:被监听事物的状态变化
- 监听器:针对事件源产生的事件的变化

#### 网络编程：

- Socket类

- 计算机网络:将地理位置不同的计算机通过通信线路连接起来,在网络操作系统、管理软件、通信协议的管理协调下，实现资源共享和信息传递
- 网络编程:不同计算机的程序进行数据交换
- iP:每台计算机的唯一标识,iPv4和iPv6是iP的取值范围和规范
- 端口号:计算机中的应用唯一标识,传输数据时不止要明确计算器,还要明确对应的程序
  - 端口范围:0-65535
- 网络协议:计算机数据交换建立的规则
  - UDP:面向无连接,不在意客户端只管发送数据,速度快
  - TCP:面向连接,需要三次握手,才会发送数据,速度慢,Http用的便是三次握手
    - TCP连接过程:三次握手
      1. 服务端发送请求
      2. 客户端响应
      3. 服务端再次确认连接
    - 为什么客户端响应后会再次确认,直接连接不可以吗,某些场景下如果服务端发送的请求后想取消.但是客户端响应后直接连接,此时会造成极大资源浪费



#### 加载类的过程

- 注意类的常量编译阶段已经确认的值,已经在编译阶段放入方法区的常量池，访问时无序加载类即可访问,但是编译阶段未赋值,需要加载类才能赋值读取

- 加载:用类加载器将该类的二进制字节流读取到JVM

- ##### 连接：

  - 验证：判断内部结构是否正确
  - 准备:为静态变量分配内存,设置默认初始化值
  - 解析:将常量池的二进制符号引用变为直接引用

- 初始化:初始化父类静态变量、执行静态代码块(与变量无优先级,与书写顺序有关)、初始化子类静态变量、静态代码块、初始化父类成员变量、构造代码块(无优先级,与书写顺序有关)、父类构造方法、子类成员变量、构造代码块、构造方法

- ##### 那些行为会加载类:

  1. 创建对象
  2. 反射
  3. 访问静态变量
  4. 访问静态方法
  5. 加载子类
  6. 使用java命令运行

- ##### 类加载器:根据一个类的全限定名将该类的二进制字节流读到JVM,然后生成一个与目标类对应的Class对象在堆中,当目标类实例创建,会自动匹配到堆中的Class对象,Class只有一个,类只加载一次

  - 根类加载器:核心类加载器
  - 拓展类加载器:拓展类加载
  - 自定义类加载:自定义类加载器

#### 反射

- 计算机含义：**反射**（英语：reflection），是指[计算机程序](https://zh.wikipedia.org/wiki/计算机程序)在[运行时](https://zh.wikipedia.org/wiki/运行时)（runtime）可以访问、检测和修改它本身状态或行为的一种能力

- 不必停止程序,程序运行中,对于任意一个类,都可以即时加载,获取和调用类的属性和方法

- 实现的原理是提前编译好相关读取代码,然后准备好类的文件,运行时读取即可

- .java文件,用java语言写的代码,jvm无法执行需要编译

- .class文件,利用jdk工具编译后二进制文件,需要jvm解释执行

- ##### 获取类所对应的Class对象

  - 类未加载阶段(.java文件):Class.forName() ,此时通过类加载器加载某个指定类(全类名:com.test.bean.Person),从而创建获取对应的Class对象
    - 只需要提前在forName()中指定文件,即可读取加载类,后期也可通过修改文件更换类
  - 加载后阶段(.class文件):类名.class,此时类所对应的Class对象已经加载后创建在堆离,此时直接获取即可
  - 实例阶段:实例.getClass(),对象创建完成后,直接获取即可
  - ![image-20221126200815878](https://raw.githubusercontent.com/1v10/Photo/main/photo/202211271215920.png)

  - [一篇了解Java反射-SecIN (sec-in.com)](https://www.sec-in.com/article/1647)

- ##### 获取Class对象后

  - getConstructor()获取构造方法:Class对象的创建实例是默认使用无参构造,可以利用该对象获取有参构造,然后创建对象

  - getField()获取成员变量,可以获取变量修改

  - getMetho获取方法,获取后可以传递参数执行方法

  - ###### 暴力反射:

    - 可以获取类的私有变量
    - 可以获取类的私有方法

  - ###### 泛型擦除

    - 泛型只在编译器有效,只为减少编译器参数类型错误,运行期会被擦除
    - 反射获取到的集合再执行添加方法将不受泛型限制

- ##### 动态代理

  - 维基百科:代理即是代表授权方处理事务

  - 代理:一个类代表另一个类执行功能

  - 静态代理(与装饰模式行为类似,目的不同):是指在程序运行前已经定义创建好目标对象以及代理对象

    - 代理对象实现目标对象的实现接口,利用组合思想,将目标对象实例,传入代理对象,重写接口方法,然后调用代理对象,再增加其他代理功能(比如日志),代理目标对象执行

  - 动态代理:程序运行时根据目标对象临时创建代理对象

    - ![image-20221126212015049](https://raw.githubusercontent.com/1v10/Photo/main/photo/202211271215194.png)

      ![image-20221126212136047](https://raw.githubusercontent.com/1v10/Photo/main/photo/202211271216314.png)

    - [(Java 动态代理作用是什么？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/20794107)

    - 利用代理类,传入目标对象类的加载器,传入目标对象的实现接口数组,传入执行的代理方法(接口形式),会返回对应代理类的Class对象,然后执行方法即可

    - Proxy:代理类

      - Proxy.newProxyInstance(目标对象类加载器,目标对象实现接口,代理功能)
        - 定义代理类的加载器:目标对象实例.class.getClassLoader()
        - 代理类要实现的接口:目标对象实例.getClass().getInterfaces()
        - 代理功能,:实现InvocationHandler接口
          - 重写InvocationHandler.invoke(代理实例,目标对象方法 method,代理实例调用方法所用参数)
            - 执行目标对象方法:method.invoke(目标对象,参数)
              - 目标对象参数需要自行传入
            - 代理对象调用目标方法会自动调用invoke方法

#### 枚举

- 列出一个有限集合的所有成员

- 单例:该类有且仅有一个实例

- 多例:该类有且仅有几个有限的实例,比如星期,性别

- ##### Enum

  - 注意 Enum也是一种特殊的类,java三种引用类型:类、接口、数组
  - 只需要大写实例名即可,会自动创建对象:MON,TUE,WED
  - 可以在Switch中使用,switch中可用:byte short int long String Enum

#### JDK7新特性

​	0x:代表十六进制

​	0b:代表二进制

#### JDK8新特性

- 接口中不再只有静态常量和抽象方法
  - 可以拥有实现方法,用default或static修饰，被称为默认方法
- 局部内部类调用局部变量,不用再给变量加final,调用默认加final



