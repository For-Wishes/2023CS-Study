# π‘ Gitκ³Ό GitHubμ λν΄μ

# β Git
## Gitμ΄λ?
- λΆμ° λ²μ  κ΄λ¦¬ μμ€ν(DVCS : Distributed Version Control System)    
    : λ³κ²½ μ¬ν­μ μΆμ νλ μμ€ν
    * Version : κ° νμΌμ μμ±λ³Έλ€(.feat μ¬λ¬ μμ λ³Έλ€β¦ ex : μ΅μ’, μ΅μ΅μ’)    
- λ‘μ»¬μμ λ²μ  κ΄λ¦¬
- μννΈμ¨μ΄ κ°λ° λ° μμ€ μ½λ κ΄λ¦¬μ μ¬μ©
- μ»΄ν¨ν° νμΌμ λ³κ²½ μ¬ν­μ μΆμ νκ³  μ¬λ¬ λͺμ μ¬μ©μλ€ κ° νμΌμ λν μμμ μ‘°μ¨νλ λ° μ¬μ©
- νμ κ΄λ¦¬ λκ΅¬(Configuration Management Tool) μ€ νλλ€.

<br/>

Gitμ λ³ΈμΈμ μ½λμ κ·Έ μμ  λ΄μ­μ κΈ°λ‘νκ³  κ΄λ¦¬νλλ‘ λλ λ²μ  κ΄λ¦¬ νλ‘κ·Έλ¨μ΄λ©°, λ‘μ»¬μμ νλ‘μ νΈμ κΈ°λ‘μ μ€μ€λ‘ κ΄λ¦¬ν  μ μλλ‘ ν΄ μ€λ€.  
Gitμ ν΅ν΄ λΈλμΉλ₯Ό μμ±νκ³  μ΄μ  λΈλμΉλ‘ λ³΅κ΅¬, μ­μ , λ³ν©μ΄ κ°λ₯νλ€. νμ§λ§ λ‘μ»¬ μ μ₯μλ₯Ό μ¬μ©νκΈ° λλ¬Έμ λ€λ₯Έ κ°λ°μμ μ€μκ°μΌλ‘ μμμ κ³΅μ ν  μ μλ€.

<br/>

μ¦, μ£Όλ‘ μ¬λ¬ λͺμ κ°λ°μκ° νλμ μννΈμ¨μ΄ κ°λ° νλ‘μ νΈμ μ°Έμ¬ν  λ, μμ€ μ½λλ₯Ό κ΄λ¦¬νλ λ° μ£Όλ‘ μ¬μ©λλ€.

<br/>

### νμ κ΄λ¦¬(Configuration Management)λ?
- λ²μ  κ΄λ¦¬(Version Management)λΌκ³ λ νλ€.  
  νμ κ΄λ¦¬ λκ΅¬λ₯Ό λ²μ  κ΄λ¦¬ μμ€νμ΄λΌκ³ λ νλ€.
- κ°μκ° κ°λ°ν μ½λ/λ¬Έμλ€μ νλμ κ΄λ¦¬ λκ΅¬μμ **ν΅ν©μ μΌλ‘ λ²μ λ³λ‘ κ΄λ¦¬**νκ² λλ κ²μ΄λ€.
- ν¬κ² μ€μμ§μ€μκ³Ό λΆμ°κ΄λ¦¬μμΌλ‘ λλλ©°  
  λνμ μΌλ‘ μ¬μ©λλ λκ΅¬λ μ€μμ§μ€μμ **SVN** κ·Έλ¦¬κ³  λΆμ°κ΄λ¦¬μμ **Git**μ΄λ€.

<br/>

### λ²μ  κ΄λ¦¬κ° νμν μ΄μ ?
> κ°λ°μ κ°μ νμμ μν΄ μ μ²΄ κ°λ° μμ€λ₯Ό κ³΅μ νλ©΄μ κ°λ° ννΈλ₯Ό λλ μ μκ³  κ°μ λͺ¨λμ κ°λ°νλλΌλ μμ€λ₯Ό κ³΅μ νλ©° κ°λ°ν  μ μκΈ° λλ¬Έμ΄λ€.
> 

<br/>

μ½λ λ²μ μ κ΄λ¦¬νλ μ΄μ λ λ€μκ³Ό κ°λ€.
1. μμ ν  λλ§λ€ νμΌ μλ‘ λ§λ€λ©΄ κ΄λ¦¬ νλ€λ€.
2. μΈμ λ  μ΄μ  λ²μ μ μ½λλ‘ λμκ° μ μκΈ° λλ¬Έμ΄λ€.
3. μ΄λ ₯μ λ¨κΈ°κΈ° μν΄ κ΄λ¦¬νλ€.
4. νλμ νλ‘μ νΈλ₯Ό λκ³  μ¬λ¬ λͺμ κ°λ°μλ€μ΄ νμν  μ μκΈ° λλ¬Έμ΄λ€.

<br/>

## Git νΉμ§
### κ°μ§μΉκΈ°(Branch)μ λ³ν©(Merge)
- μ¬μ©μλ λ©μΈ μ½λμμ κ°μ§λ₯Ό μμ±ν΄μ λλ¦½μ±μ μ μ§ν νλ‘ κ°λ°μ μ§νν  μ μλ€. μ΄λ λ€μν μ½λλ₯Ό κ°λ° λλ νμ€νΈ ν΄ λ³Ό μ μλ νκ²½μ μ κ³΅ν΄ μ€λ€.
- μ¬λ¬ κ°μ§λ₯Ό λ§λ€μ΄ κ°λ° λλ νμ€νΈλ₯Ό μ§νν  μ μκ³  μ΄ν λ³ν©μ ν΅ν΄ λ©μΈ μ½λμ λ°μμ νκ±°λ μ­μ ν  μ μλ€.
- κ°μ§λ μΌ λ¨μμ μμμ΄ λ  μλ μκ³ , κΈ°λ₯μ΄ λ  μλ μλ€. μ¬μ©νκΈ° λλ¦μ΄λ€.

<br/>

### κ°λ³κ³  λΉ λ₯΄λ€
- Gitμ λͺ¨λ  μμμ΄ λλΆλΆ λ‘μ»¬μμ μ§νλλ€.
- λ§€λ² λ€νΈμν¬μ μ μν  νμκ° μκΈ° λλ¬Έμ λλΆλΆμ μμμ΄ λ€νΈμν¬ μλμ κ΄κ³μκ³ , λ§€μ° λΉ λ₯΄κ² μ§νλλ€.

<br/>

### λΆμ° μμ
- Gitμ λΆμ° μμμ ν¨μ¨μ μ΄λ€. μ¬μ©μλ€μ λ³΅μ¬λ νλ‘μ νΈμμ λμμ μμμ μ§νν  μ μλ€.
- λν κ°κ°μ μ¬μ©μλ€μ λ©μΈ μ½λ μ μ²΄λ₯Ό κ°μ§κ³  μλ€. μλ²κ° λ€μ΄λλ λ±μ λ¬Έμ κ° λ°μνλλΌλ μ¬μ©μ κ°κ°μ μ½λ μ μ²΄λ₯Ό κ°μ§κ³  μκΈ° λλ¬Έμ λ¬Έμ κ° λ°μν  μμ§κ° μλ€.
- Gitμ νΉμ±κ³Ό μ°μν λΆκΈ° μμ€ν λλΆμ κ±°μ λ¬΄νλμ μν¬ νλ‘λ₯Ό μλμ μΌλ‘ μ½κ² κ΅¬νν  μ μλ€.
- λλλ‘ μμ€ μ½λλ₯Ό λ³ν©νλ λ° μμ΄μ λ²κ±°λ‘μμ λλ μλ μμ΄, Gitμμλ ν΅ν© κ΄λ¦¬μλ₯Ό λμ΄ μ­ν  λΆλ΄μ ν  μ μλ€. μ¬μ©μλ μμ€ μ½λμ ν΅ν©μ λ§μ μ κ²½μ μ°μ§ μμλ λκ³ , λ§‘μ μ­ν μλ§ μ§μ€ν  μ μλ€.

<br/>

### λ°μ΄ν° λ³΄μ₯
- Gitμ νλ‘μ νΈμ λ¬΄κ²°μ±μ λ³΄μ₯νλ€. λͺ¨λ  νμΌμ μ²΄ν¬μ¬μ΄λΌλ κ²μ¬λ₯Ό κ±°μΉκ² λλ€.
- μ²΄ν¬μ¬μ 16μ§μ λ¬Έμμ΄λ‘ κ΅¬μ±λμ΄ μμΌλ©°, Commit IDλΌκ³  λΆλ¦°λ€. Commit IDκ° κ°μ κ²μ νμΌ λλ κ΅¬μ±μ΄ μλ²½ν κ°λ€λ κ²μΌλ‘, Commit IDλ κ°μλ° νμΌ λλ κ΅¬μ±μ΄ λ€λ₯Ό μ μλ€.
- μ΄λ₯Ό ν΅ν΄ λκ° μ΄λ νμΌμ μμνλμ§ κΈ°λ‘μ΄ λ¨κΈ° λλ¬Έμ Version history κ΄λ¦¬λ ν  μ μλ€.

<br/>

### μ€λΉ μμ­
- Gitμ μ€λΉ μμ­μ κ°μ§κ³  μλ€. μ΄λ μμ ν λ΄μ©μ λ°μνκΈ° μ  κ²ν νλ λ¨κ³λΌκ³  ν  μ μλ€.
- μμ λλ ν°λ¦¬μμ λ°μν  νμΌμ μ ννκ³  μ΄ν μμ ν νμΌμ μ€μ λ‘ μ μ₯μμ λ°μνλ 2λ¨κ³λ₯Ό κ±°μ³μΌ μλ£λλ€.
- λ¬Όλ‘  μμ ν νμΌ μ€ μ μ₯μμ λ°μν  νμΌλ§ μ ννλ κ²λ κ°λ₯νλ€.

<br/>

### μ€ν μμ€
- Gitμ μ€ν μμ€λ€. μμμ μΈκΈν μ₯μ μ κ·Έλλ‘ κ°μ§κ³  μμΌλ©΄μ κ³μ λ°μ ν΄ λκ°κ³  μλ€.

<br/>

### Git νΈμ€ν μλΉμ€
- GitHub
- Atlassian Bitbucket
- GitLab

<br/>

## Git μ₯λ¨μ 
### Git μ₯μ 
- λΆμ°μ μΈ κ°λ°  
    : κΉ(Git)μ μ¬μ©νλ μ μ²΄ κ°λ° λ΄μ­μ κ° κ°λ°μμ λ‘μ»¬ μ»΄ν¨ν°λ‘ λ³΅μ¬ν  μ μλ€.  
    λμ€μ μλ‘ μμ λ λ΄μ­μ ν©μΉκΈ°(Merge) ν  μλ μμΌλ©°, μ΄ λ Gitμ κ³ μ ν νλ‘ν μ½μ μ΄μ©νκ² λλ€.
- ν¨μ¨μ μΈ κ°λ°  
    : κΉ(Git)μ μΌλ°μ μΈ λ€λ₯Έ λ²μ  κ΄λ¦¬ μμ€νλ³΄λ€ μ±λ₯μ΄ λ°μ΄λλ©°, λ³κ²½ μ΄λ ₯μ΄ λ§λλΌλ λ³κ²½λ λ΄μ©λ§ μ²λ¦¬νλ€λ μ μμ λ©λͺ¨λ¦¬μ μΈ ν¨μ¨μ±μ΄ λ°μ΄λλ€.
- λΉμ νμ μΈ κ°λ°  
    : κΉ(Git)μ λΈλμΉ(Branch)λΌλ κ°λμ΄ μ¬μ©λλ€. λ€μ λ§ν΄μ νλ‘μ νΈμ κ°μ§μΉκΈ°κ° κ°λ₯νλ€λ λ»μ΄λ€.  
    μ΄λ νΈλ¦¬ κ΅¬μ‘°, λ€μ λ§ν΄μ λΉμ νμ μΈ κ΅¬μ‘°λΌκ³  λ³Ό μ μλ€.
- λ³κ²½ μ΄λ ₯ λ³΄μ₯  
    : μμλ λͺ¨λ  λ΄μ­(Commit λ΄μ­)λ€μ λͺ¨λ λ³λμ μμ­μμ κ΄λ¦¬λμ΄ μμ νκ² νλ‘μ νΈλ₯Ό μ΄μν  μ μλ€.
- μ²λ¦¬ μλκ° λΉ λ₯΄λ€.
- νμ μ©μ΄μ±
- μλ¬ μ λ³΅κ΅¬κ° μ©μ΄νλ€.

<br/>

### Git λ¨μ 
- μ§κ΄μ μ΄μ§ μλ€.  
    : κ³΅μ  κ³Όμ μ΄ λΉκ΅μ  λ³΅μ‘νλ€. μ΄λ μλμ μΈ κ²μΌλ‘ Gitμ λν΄ GUIλ₯Ό μ κ³΅ν΄ μ£Όλ GitHub Desktop λ±μ μ¬μ©νλ©΄ μ΄λ ΅μ§ μλ€.

<br/>

## Git κΈ°λ³Έ μ©μ΄
### Repository
- μ μ₯μ
- μ μ₯μλ νμ€ν λ¦¬, νκ·Έ, μμ€μ κ°μ§μΉκΈ° νΉμ branchμ λ°λΌ λ²μ μ μ μ₯νλ€.
- μμμκ° λ³κ²½ν λͺ¨λ  νμ€ν λ¦¬λ₯Ό νμΈ κ°λ₯νλ€.

<br/>

### Working Tree
- μ μ₯μλ₯Ό μ΄λ ν μμ μΌλ‘ λ°λΌλ³΄λ μμμμ νμ¬ μμ 
- νμΌ μμ , μ μ₯ λ±μ μμμ νλ λλ ν°λ¦¬

<br/>

### Staging Area
- μ»€λ°μ μ€ννκΈ° μ μ μ μ₯μμ μμ νΈλ¦¬ μ¬μ΄μ μ‘΄μ¬νλ κ³΅κ°

<br/>

### Commit
- νμ¬ λ³κ²½λ μμ μνλ₯Ό μ κ²μ λ§μΉλ©΄ νμ νκ³  μ μ₯μμ μ μ₯νλ μμ

<br/>

### Head
- νμ¬ μμ μ€μΈ Branchλ₯Ό κ°λ¦¬ν¨λ€.

<br/>

### Branch
- κ°μ§ λλ λΆκΈ°μ 
- μμμ ν  λ, νμ¬ μνλ₯Ό λ³΅μ¬νμ¬ Branchμμ μμμ νλ€.  
  κ·Έ ν, μμ νλ€ μΆμ λ Mergeλ₯Ό νμ¬ μμμ νλ€.

<br/>

### Merge
- λ€λ₯Έ Branchμ λ΄μ©μ νμ¬ Branchλ‘ κ°μ Έμ ν©μΉλ μμμ μλ―Ένλ€.

<br/>

## Git λͺλ Ήμ΄
### Git κΈ°λ³Έ λͺλ Ήμ΄
- git help : λμλ§ κΈ°λ₯(κ°μ₯ λ§μ΄ μ¬μ©νλ 21κ°μ Git λͺλ Ήμ΄ μΆλ ₯)μ΄λ€. μ¬μ©λ²μ΄ κΆκΈν λͺλ Ήμ΄μ λν΄ βgit help [κΆκΈν λͺλ Ήμ΄]βλ₯Ό νμ΄ν μ, ν΄λΉ Git λͺλ Ήμ΄μ μ€μ κ³Ό μ¬μ©μ λν λμλ§μ μΆλ ₯νλ€.
- git init : Git μ μ₯μλ₯Ό μ΄κΈ°ννλ€. μ μ₯μλ λλ ν°λ¦¬ μμμ μ΄ λͺλ Ήμ μ€ννκΈ° μ κΉμ§λ κ·Έλ₯ μΌλ° ν΄λμ΄λ€. μ΄ λͺλ Ήμ΄λ₯Ό μλ ₯ν νμμΌ μΆκ°μ μΈ Git λͺλ Ήμ΄ μλ ₯μ΄ κ°λ₯νλ€.
- git status : μ μ₯μ μνλ₯Ό μ²΄ν¬νλ€. μ΄λ€ νμΌμ΄ μ μ₯μ μμ μλμ§, μ»€λ°μ΄ νμν λ³κ²½ μ¬ν­μ΄ μλμ§, νμ¬ μ μ₯μμ μ΄λ€ λΈλμΉμμ μμνκ³  μλμ§ λ±μ μν μ λ³΄λ₯Ό μΆλ ₯νλ€.
- git branch : μλ‘μ΄ λΈλμΉλ₯Ό μμ±νλ€. μ¬λ¬ νμμμ μμν  μ, μ΄ λͺλ Ήμ΄λ‘ μλ‘μ΄ λΈλμΉλ₯Ό λ§λ€κ³ , μμ λ§μ λ³κ²½ μ¬ν­κ³Ό νμΌ μΆκ° λ±μ μ»€λ° νμλΌμΈμ μμ±νκ³ , μμ± ν νμμμ branch νΉμ mainκ³Ό mergeνλ€.
- git add : βstaging μμ­βμ λ³κ²½ λ΄μ©μ μΆκ°νλ€. λ€μ commit λͺλ Ή μ κΉμ§ λ³κ²½λΆμ staging μμ­μ λ³΄κ΄νμ¬ λ³λ λ΄μ­μ μ μ₯νλ€.
        
    | λͺλ Ήμ΄ | μμ© |
    | --- | --- |
    | git add [μλ‘λνκ³  μΆμ νμΌ νΉμ λλ ν°λ¦¬ κ²½λ‘] | ν΄λΉ νμΌ νΉμ λλ ν°λ¦¬ λ³κ²½ λ΄μ© staging area λ±λ‘ |
    | git add . | νμ¬ λλ ν°λ¦¬ λͺ¨λ  λ³κ²½ λ΄μ© staging area λ±λ‘(μμ X) |
    | git add -A | μμ λλ ν°λ¦¬ λͺ¨λ  λ³κ²½ λ΄μ© staging area λ±λ‘ |
    | git add -p | ν°λ―Έλμμ staging areaλ‘ λκΈΈ νμΌ μ ν κ°λ₯ |
- git commit : staging areaμ μλ λ³κ²½ λ΄μ© λ¬Άμ λ° μ μ, Gitμ κ°μ₯ μ€μν λͺλ Ήμ΄λ€.  
  * cf : `git commit -m βμ»€λ° λ©μμ§β` ν΄λΉ λͺλ Ήμ΄μ staging areaμ μλ λ΄μ©μ βμ»€λ° λ©μμ§βλ₯Ό λ°μν μμ λ³Έ νμΌμ λ¬Άμμ΄λ€.
- git log : μ»€λ° λ΄μ­ νμΈ
- git push : λ‘μ»¬ μ»΄ν¨ν°μμ μλ²λ‘ λ³κ²½ μ¬ν­μ pushνλ€.
- git pull : μλ² μ μ₯μλ‘λΆν° μ΅μ  λ²μ μ pullνλ€.(μλ² μ μ₯μμ λ°μ΄ν°λ₯Ό κ°μ Έμ νμ¬ λΈλμΉμ mergeνλ€.)  
  * cf : μμ λμ€ κΈ°μ‘΄ μμ λ΄μ©μ μ μ§νλ©΄μ μ΅μ  μ½λλ‘ μλ°μ΄νΈν  λ μ¬μ©νλ€.
- git clone : μλ² μ μ₯μμ λ°μ΄ν°λ₯Ό λ‘μ»¬ μ»΄ν¨ν°λ‘ λ³΅μ¬νλ€.(μλ² μ μ₯μμ λ°μ΄ν°λ₯Ό κ·Έλλ‘ κ°μ Έμ¨λ€. μμ μ€μ΄λ λ΄μ­μ΄ μμ μ λ?μ΄μ°κΈ° λλ€.)  
  * cf : νλ‘μ νΈμ μ²μ ν¬μλ  λ μ¬μ©
- git checkout : μμνκΈ° μνλ λΈλμΉλ‘ μ΄λνλ€.  
  * cf : `git checkout SH` : SH λΈλμΉλ‘ μ΄λνλ€.  
  * cf : `git checkout -b PSH` : βPSHβλΌλ λΈλμΉλ₯Ό μμ± ν PSH λΈλμΉλ‘ μ΄λνλ€.(μμ±κ³Ό μ΄λμ λμμ νλ€.)
- git merge : κ°λ³ branchμμ λ§μΉ μμμ master branchλ‘ λ³ν©νλ€.

<br/>

### git init κ³Ό git cloneμ μ°¨μ΄
- git init : λΉ Git μ μ₯μλ₯Ό λ§λ€κ±°λ κΈ°μ‘΄ μ μ₯μλ₯Ό λ€μ μ΄κΈ°ννλ λͺλ Ήμ΄.
- git clone : μκ²©μ Git μ μ₯μλ₯Ό λ‘μ»¬μ λ³΅μ ν΄μ€λ λͺλ Ήμ΄.

<br/>

> git initμ νλ‘μ νΈ μμ²΄λ₯Ό μ²μλΆν° μμνλ κ²μ΄κ³ ,  
git cloneμ νλ‘μ νΈ λ΄μ μ€κ° ν¬μμ΄ κ°λ₯νλ©° clone μ λ€μ init ν΄ μ€ νμκ° μλ€.
> 

<br/>

### commit message type
- Add : λ μ΄μμ/κΈ°λ₯ μΆκ° ex) Add : login λ μ΄μμ
- Remove : λ΄μ© μ­μ (ν΄λ/νμΌ μ­μ )
- Modify : μμ (JSON λ°μ΄ν° ν¬λ§· λ³κ²½ / λ²νΌ μκΉ λ³κ²½ / ν°νΈ λ³κ²½)
- Fix : λ²κ·Έ/μ€λ₯ ν΄κ²°
- Refactor : μ½λ λ¦¬ν©ν λ§(λ©ν  λ¦¬λ·° λ°μ / μ€μ€λ‘ λ¦¬ν©ν λ§ / μ€λ³΅ μ½λ μ κ±° / λΆνμ μ½λ μ κ±° / μ±λ₯ κ°μ )
- Docs : λ¬Έμμ κ΄λ ¨λ μμ  μμ(README.md λ±)

<br/>
<br/>

# **β** GitHub
## GitHubλ?
- Git Repositoryλ₯Ό μν μΉ κΈ°λ° νΈμ€ν μλΉμ€
- ν΄λΌμ°λ μλ²λ₯Ό μ¬μ©ν΄μ λ‘μ»¬μμ λ²μ  κ΄λ¦¬ν μμ€ μ½λλ₯Ό μλ‘λνμ¬ κ³΅μ  κ°λ₯
- λΆμ° λ²μ  μ μ΄, μ‘μΈμ€ μ μ΄, μμ€ μ½λ κ΄λ¦¬, λ²κ·Έ μΆμ , κΈ°λ₯ μμ²­ λ° μμ κ΄λ¦¬λ₯Ό μ κ³΅

<br/>

GitHubλ Git μ μ₯μλ₯Ό κ΄λ¦¬νλ ν΄λΌμ°λ κΈ°λ° νΈμ€ν μλΉμ€λ€.  
Git μ μ₯μ νΈμ€ν μλΉμ€λ ν΄λΌμ°λ κΈ°λ°μΌλ‘ λ€λ₯Έ μ¬λκ³Ό μμ€ μ½λ κ³΅μ κ° κ°λ₯νλ©° Gitμ κΈ°λ³Έμ μΈ κΈ°λ₯μ νμ₯νμ¬ μ κ³΅νλ€. λν ν΄λΌμ°λ μλ²μ μμ€λ₯Ό μ¬λ¦¬κΈ° λλ¬Έμ ν νλ‘μ νΈμ μ¬λ¬ λͺμ μ¬λμ΄ μ°Έμ¬νμ¬ λ²μ  μ μ΄ λ° κ³΅λ μμμ΄ κ°λ₯νλ€.

<br/>
<br/>

# β Gitκ³Ό GitHubμ μ°¨μ΄
Gitμ λ²μ  κ΄λ¦¬ 'νλ‘κ·Έλ¨'μ΄κ³ ,  
GitHubλ λ²μ  κ΄λ¦¬, μμ€ μ½λ κ³΅μ , λΆμ° λ²μ  μ μ΄ λ±μ΄ κ°λ₯ν μκ²© μ μ₯μλ€.

<br/>
<br/>

# π μ°Έκ³ 

- [[Git] κΉ(Git)κ³Ό κΉνλΈ(Github) μ°¨μ΄ :: μ½λ© κ³΅λΆ μΌμ§ (tistory.com)](https://cocoon1787.tistory.com/723)
- [[Git]gitκ³Ό github μ λλ‘ μ΄ν΄νκΈ°! (velog.io)](https://velog.io/@hoje15v/git%EA%B3%BC-github-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
- [[git] gitμ΄λ? (νμκ΄λ¦¬, μ μ, μ₯λ¨μ , μ€μΉ) (velog.io)](https://velog.io/@lazysia/git-git)
- [[μΉκ°λ° κΈ°μ΄] Git μ΄λ? (tistory.com)](https://goddaehee.tistory.com/91)
- [GITμ¬μ©λ²- (5)Gitμ νΉμ§. Gitμ νΉμ§ | by νμ΄ | Medium](https://medium.com/@what_learn/git%EC%82%AC%EC%9A%A9%EB%B2%95-5-git%EC%9D%98-%ED%8A%B9%EC%A7%95-216da8d443d7)
- [[Github] κΈ°μ΄ λ΄μ© μ΄μ λ¦¬ - 1 - Gitμ΄λ? Gitμ νΉμ§ (tistory.com)](https://chancoding.tistory.com/166)
- [[GIT] git λ±μ₯ λ°°κ²½κ³Ό μ₯μ  (tistory.com)](https://power-girl0-0.tistory.com/342)
- [[git] gitμ΄λ? (νμκ΄λ¦¬, μ μ, μ₯λ¨μ , μ€μΉ) (velog.io)](https://velog.io/@lazysia/git-git)
- [[Git] κΉ(git)κ³Ό κΉνλΈ(github)λ λ¬΄μμΈκ°? (tistory.com)](https://yanacoding.tistory.com/4)
- [Git ν·κ°λ¦¬λ κ°λμ‘κΈ°2 - Repository(repository, git directory, work tree, index, staging area), branch, master, origin, upstream :: nemo's dev memos (tistory.com)](https://nemomemo.tistory.com/87)
- [[GIT]Working Tree(μμ νΈλ¦¬) (tistory.com)](https://developer-ankiwoong.tistory.com/763)

