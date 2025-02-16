# Arvore-Binaria-de-Busca

## MUDANÇAS E ALTERAÇÕES

### **função inserir na main**
Por conta da possível modificação da raiz, foi necessário a reatribuição da raiz a cada chamada da função inserir para garantir que a raiz possivelmente atualizada seja corretamente considerada.
```
    raiz = inserir(raiz, 10); //reatribuindo a raiz porque a funcao pode retornar um novo ponteiro para a raiz em caso de modificacao
    raiz = inserir(raiz, 5);
    raiz = inserir(raiz, 15);
    raiz = inserir(raiz, 10); // repetido => contador(10)++
    raiz = inserir(raiz, 5);  // repetido => contador(5)++
    raiz = inserir(raiz, 5);  // repetido => contador(5)++
    raiz = inserir(raiz, 18);
```
```
    raiz = inserir(raiz, 12);
    raiz = inserir(raiz, 16);
    raiz = inserir(raiz, 3);
```
### **função lowestCommonAncestor**
O resultado esperado de `nLCA = lowestCommonAncestor(raiz, 16, 18);` é 15, mas o 16 inserido na árvore se torna filho do 18, visto que é maior que 15, assim, o resultado de `nLCA = lowestCommonAncestor(raiz, 16, 18);` é, na realidade, o próprio 18.
```
    nLCA = lowestCommonAncestor(raiz, 16, 18);                           //chave 18 encontrada, visto que 16 é filho do 18
    if(nLCA) {
        printf("LCA(16,18) => chave=%d (esperado=15)\n", nLCA->chave);
    }
```

*No código o 16 é supostamente fiho do 12, quando deveria ser filho do 18, já que 16 é maior que 15 e deveria ter ido à direita da árvore:*
```
    // 8) Testar LCA (lowestCommonAncestor) - não é opcional
    //    Vamos inserir mais alguns valores para teste de LCA
    //    Situação final da árvore atual: 5(cont=2),15(cont=1),18(cont=1)
    //    Inserir(12), Inserir(16), Inserir(3)
    //    Nova BST (com contadores):
    //       5 (cont=2)
    //           /    \
    //         3(1)   15(1)
    //                /  \
    //              12(1) 18(1)
    //                  \
    //                  16(1)
```

O resultado esperado de `nLCA = lowestCommonAncestor(raiz, 5, 18);` é 5, mas a chave 15 é encontrada, por conta da mudança da raiz ocorrida em `removerTodasOcorrencias` após todos os nós da chave 10 serem removidos, ou seja, a raiz é removida, e o seu sucessor(15) se tornar a raiz. 
```
nLCA = lowestCommonAncestor(raiz, 5, 18);                            // chave 15 encontrada, raiz mudou de 10 para 15
    if(nLCA) {
        printf("LCA(5,18) => chave=%d (esperado=5)\n", nLCA->chave);
    }
```
