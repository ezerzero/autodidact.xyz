---
date: 2018-11-07 02:38:21 +0800
category: programming
permalink: /c3-linearization
---
# C3 Linearization

class B(A1,A2,A3 ...)  
mro(B) = [B] + merge(mro(A1), mro(A2), mro(A3) ..., [A1,A2,A3])  
MRO: Method Resolution Order  
遍历执行merge操作的序列，如果一个序列的第一个元素，在其他序列中也是第一个元素，或不在其他序列出现，则从所有执行merge操作序列中删除这个元素，合并到当前的mro中。  
merge操作后的序列，继续执行merge操作，直到merge操作的序列为空。  
如果merge操作的序列无法为空，则说明不合法。

    class A(O):pass
    class B(O):pass
    class C(O):pass
    class E(A,B):pass
    class F(B,C):pass
    class G(E,F):pass
    mro(A) = [A] + merge(mro(O),[O])
           = [A] + merge([O], [O])
           = [A,O]
    mro(B) = [B] + merge(mro(O),[O])
           = [B] + merge([O], [O])
           = [B,O]
    mro(C) = [C] + merge(mro(O),[O])
           = [C] + merge([O], [O])
           = [C,O]
    mro(E) = [E] + merge(mro(A), mro(B), [A,B])
           = [E] + merge([A,O], [B,O], [A,B])
           = [E,A] + merge([O], [B,O], [B])
           = [E,A,B] + merge([O], [O])
           = [E,A,B,O]
    mro(F) = [F] + merge(mro(B), mro(C), [B,C])
           = [F] + merge([B,O], [C,O], [B,C])
           = [F,B] + merge([O], [C,O], [C])
           = [F,B,C] + merge([O], [O])
           = [F,B,C,O]
    mro(G) = [G] + merge(mro[E], mro[F], [E,F])
           = [G] + merge([E,A,B,O], [F,B,C,O], [E,F])
           = [G,E] + merge([A,B,O], [F,B,C,O], [F])
           = [G,E,A] + merge([B,O], [F,B,C,O], [F])
           = [G,E,A,F] + merge([B,O], [B,C,O])
           = [G,E,A,F,B] + merge([O], [C,O])
           = [G,E,A,F,B,C] + merge([O], [O])
           = [G,E,A,F,B,C,O]

来源：[http://blog.sina.com.cn/s/blog\_45ac0d0a01018488.html](http://blog.sina.com.cn/s/blog_45ac0d0a01018488.html)
