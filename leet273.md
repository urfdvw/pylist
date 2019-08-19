# [273. Integer to English Words](https://leetcode.com/problems/integer-to-english-words/)
Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than 2^31 - 1.

Example
```
123 -> "One Hundred Twenty Three"
12345 -> "Twelve Thousand Three Hundred Forty Five"
1234567 -> "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```
## Solution
```python
class Solution:
    def numberToWords(self, num):
        """
        :type num: int
        :rtype: str
        """
        # exception
        if num == 0:
            return 'Zero'
        text = str(num)
        # group by 3 digits
        group = []
        while len(text) > 3:
            group.append(text[-3:])
            text=text[0:-3]
        group.append(text[-3:])
        # convert each item to number 
        group = [int(n) for n in group]
        print(group)
        titles = ['','Thousand','Million','Billion']
        words = []
        for i in range(4):
            try:
                currentword = self.within1000(group[i])
                if currentword != []:
                    currentword.append(titles[i])
                words = currentword + words
                print(currentword)
            except:
                pass
        words = [w for w in words if len(w)>0]
        return ' '.join(words)
        
    
    def within1000(self,num): 
        if num == 0:
            return []
        
        words = []
        
        numberNames = ['One','Two','Three','Four','Five','Six','Seven','Eight','Nine','Ten',\
                      'Eleven','Twelve','Thirteen','Fourteen','Fifteen','Sixteen','Seventeen','Eighteen','Nineteen']
        tys = ['Twenty','Thirty','Forty','Fifty','Sixty','Seventy','Eighty','Ninety']

        g100,l100 = divmod(num,100)
        
        if g100 != 0:
            g100T = [ numberNames[g100 - 1], 'Hundred']
        else:
            g100T = []
            
        if l100 != 0:
            if l100 <= 19:
                l100T = [numberNames[l100 - 1]]
            else:
                g10,l10 = divmod(l100,10)
                print(g10,l10)
                if l10 != 0:
                    l100T = [tys[g10 - 2],numberNames[l10 -1]]
                else:
                    l100T = [tys[g10 - 2]]
        else:
            l100T = []
        g100T.extend(l100T)
        return g100T
```