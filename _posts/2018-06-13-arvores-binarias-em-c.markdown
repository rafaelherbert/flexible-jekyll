---
layout: post
title: "Arvores binárias em C"
date: 2018-06-18
description: Conceito e aplicação de árvores binárias na linguagem C.
img: c.jpg # (Optional)
fig-caption: C Programming Language # (Optional)
tags: [C, binary trees] # (Optional)
---

As árvores binárias são uma estrutura de dados de uma quantidade finita de elementos onde o primeiro nó é chamado de **Raiz**, e os outros nós são divididos em subconjuntos distintos, onde cada um forma uma árvore binária. Cada elemento é um **Nó (ou vértice)**. Cada nó de uma árvore binária possui um valor e dois ponteiros, o da direita e o da esquerda, que apontam para os próximos dois nós da árvore binária.

## Terminologia
- Pai
  - Todo nó que possui um ou mais sucessores.
- Filho
  - Todo nó que possui um antecessor imediato.
- Irmãos
  - Filhos de um mesmo pai.
- Pais com pelo menos um filho
  - Não terminais ou internos.
- Caminho
  - Uma lista de nós distintos e sucessivos conectados através da árvore.
- Nó Raiz
  - O Nó no qual partem todos os caminhos da árvore.

## Propriedades
- Grau de um nó
  - É o número de filhos de um nó.
- Nível de um nó
  - Número de nós no caminho entre o nó e a raiz. (A raiz possui índice 0).
- Altura da árvore
  - Corresponde ao nó com o maior nível.
- Árvore Binária Estrita
  - Um árvore binária estrita é aquela em que todo nó não folha possui filhos à esquerda e à direita (Dois filhos).
- Árvore Binária Cheia
  - Uma árvore binária cheia é aquela em que todas as folhas se encontram no nível d (Último nível).
- Árvore Binária Completa
  - Uma árvore binária cheia é aquela em que todas as folhas se encontram ou no nível d (Penúltimo nível), ou no nível d-1 (Penúltimo nível).


## Operações em árvores binárias

#### Estrutura do nó da árvore binária
```c
typedef struct node {
  	int dado;
  	struct node *esq;
 	struct node *dir;
	struct node *pai;
} Node;
```

#### esquerda(raiz)
##### Retorna o ponteiro que aponta para o filho à esquerda.

```c
Node* esquerda(Node *raiz)
{
	Node *aux = raiz;
	if (aux->esq != NULL)
		aux = aux->esq;
	else
		return NULL;
	return aux;
}
``` 

#### direita(raiz)
##### Retorna o ponteiro que aponta para o filho à direita.
```c
Node* esquerda(Node *raiz)
{
	Node *aux = raiz;
	if (aux->dir != NULL)
		aux = aux->dir;
	else
		return NULL;
	return aux;
}
```

#### pai(raiz)
##### Retorna o ponteiro que aponta para o pai do nó inserido.
```c
Node* esquerda(Node *raiz)
{
	Node *aux = raiz;
	if (aux->pai != NULL)
		aux = aux->pai;
	else
		return NULL;
	return aux;
}
```


#### irmao(raiz)
##### Retorna o ponteiro que aponta para o irmão do nó inserido
```c
Node* irmao(Node *raiz)
{
	Node *aux = raiz;
	
	if(aux == aux->pai->esq){
		if(aux->pai->dir != NULL){
			aux = aux->pai->dir;
			return aux;
		}
		else {
			return NULL;
		}
	}
	
	if(aux == aux->pai->dir){
		if(aux->pai->esq != NULL){
			aux = aux->pai->esq;
			return aux;
		} else {
			return NULL;
		}
	}

}

```

#### criaAB(dado)
##### Cria uma árvore binária com a raiz com o dado inserido, e a retorna.
```c
Node* criaAB(int dado)
{
	// Aloca memória para o novo nó.
	Node *node = (Node*)malloc(sizeof(Node));
	// Define o dado do nó.
	node->dado = dado;
	// Inicializa os filhos da esquerda e direita e o pai como NULL.
	node->esq = NULL;
	node->dir = NULL;
	node->pai = NULL;
	return node;
}
```

#### filhoEsq(raiz)
##### Cria um filho à esquerda do nó inserido, retorna 1 se conseguir e 0 se falhar.
```c
int filhoDir(Node *raiz, int dado)
{
	Node *node = criaAB(dado);
	if (raiz->esq == NULL){
		raiz->esq = node;
		raiz->esq->pai = raiz;
		return 1;
	} else {
		return 0;
	}
}
```

#### filhoDir(raiz)
##### Cria um filho à direita do nó inserido, retorna 1 se conseguir e 0 se falhar.
```c
int filhoDir(Node *raiz, int dado)
{
	Node *node = criaAB(dado);
	if (raiz->dir == NULL){
		raiz->dir = node;
		raiz->dir->pai = raiz;
		return 1;
	} else {
		return 0;
	}
}
```


## Percorrendo árvores binárias

Existem 3 diferentes métodos para percorrer uma árvore binária:
1. Pré ordem
   - Visitar a raiz, depois a subárvore da esquerda, e logo após a subárvore da direita. 
2. Em ordem
   - Visitar a subárvore da esquerda, depois a raiz, depois a subárvore da direita. 
3. Pós ordem
   - Visitar as subárvores da esquerda e direita, e depois visitar a raiz. 

Vamos ver como esses códigos seriam implementados:

#### pre_ordem(raiz)
```c
void pre_ordem(Node *raiz)
{
	if (raiz == NULL) return;
	printf("%d\n", raiz->dado);
	pre_ordem(raiz->esq);
	pre_ordem(raiz->dir);
}
```

#### em_ordem(raiz)
```c
void em_ordem(Node *raiz)
{
	if (raiz == NULL) return;
	pre_ordem(raiz->esq);
	printf("%d\n", raiz->dado);
	pre_ordem(raiz->dir);
}
```

#### pos_ordem(raiz)
```c
void pos_ordem(Node *raiz)
{
	if (raiz == NULL) return;
	pre_ordem(raiz->esq);
	pre_ordem(raiz->dir);
	printf("%d\n", raiz->dado);
}
```


 Para ilustrar o funcionamento desse algoritmo, vamos observar o comportamento do seu retorno quando aplicado a seguinte árvore binária:
 ![Arvores binárias exemplo 1]({{ "/assets/img/bt_example_1.png" | absolute_url }})

#### Aplicando o algoritmo pré_ordem temos o retorno:
10<br>
7<br>
3<br>
2<br>
15<br>
2<br>
11<br>

#### Aplicando o algoritmo em_ordem temos o retorno:
7<br>
3<br>
2<br>
10<br>
15<br>
2<br>
11<br>

#### Aplicando o algoritmo pré_ordem temos o retorno:
7<br>
3<br>
2<br>
15<br>
2<br>
11<br>
10

## Árvores binárias de busca

Árvores binárias de busca são árvores binárias ordenadas de acordo com o dado que cada nó possui. Se um nó possui dado maior do que o nó pai, então ele será inserido à direita, se for menor, será inserido à esquerda, e assim, a árvore é constituída de forma ordenada.

### Operações em árvores binárias de busca

#### buscaAB(Node \*raiz, int dado)
##### Busca um valor específico na árvore binária de busca. Se o valor for encontrado, retorna 1, se não, retorna 0.
```c
int buscaAB(Node *raiz, int dado)
{
	if (raiz->dado == dado)
		return 1;
	else {
		if (dado > raiz->dado)
			raiz = direita(raiz);
		else
			raiz = esquerda(raiz);
		
		if (raiz == NULL) return 0;
		buscaAB(raiz, dado);
	}
}
``` 

#### insereAB(Node \*raiz, int dado)
##### Insere um novo nó com o valor dado na árvore binária de busca raiz, retorna 1 no sucesso, e 0 se um nó com o mesmo valor já estiver alocado.
```c
int insereAB(Node *raiz, int dado)
{
	if (raiz -> dado == dado)
		return 0
	else {
		if (dado > raiz->dado){
			if (direita(raiz) != NULL){
				raiz = direita(raiz);
				insereAB(raiz, dado);
			}
			else {
				filhoDir(raiz, dado);
				return 1;
			}
		} else {
			if (esquerda(raiz) != NULL){
				raiz = esquerda(raiz);
				insereAB(raiz, dado);
			}
			else {
				filhoEsq(raiz, dado);
				return 1;
			}
		}
	}
}
``` 

#### removeAB(Node \*raiz, int dado)
##### Remove o nó com o valor dado da árvore binária de busca raiz. 
```c
int removeAB(Node *raiz, int dado)
{
	Node *pai = raiz;
	
	while (raiz != NULL && raiz->dado != dado){
		pai = raiz;
		if (dado > raiz->dado) raiz = direita(raiz);
		else raiz = esquerda(raiz);
	}
	
	if (raiz != NULL) {
		// Se tiver duas subárvores.
		if (esquerda(raiz) != NULL && direita(raiz) != NULL){
			Node *aux = raiz;
			pai = raiz;
			raiz = direita(raiz);
			while(esquerda(raiz) != NULL){
				pai = raiz;
				raiz = esquerda(raiz);
			}
			aux->dado = raiz->dado;
		}
		//É importante que esse próximo if não seja um "else if".
		//Se tiver uma subárvore à esquerda.
		if (esquerda(raiz) == NULL && direita(raiz) != NULL){
			if (pai->esq == raiz) pai->esq = direita(raiz);
			else pai->dir = direita(raiz);
		}
		//Se tiver uma subárvore à direita.
		else if (esquerda(raiz) != NULL && direita(raiz) == NULL) {
			if (pai->esq == raiz) pai->esq = esquerda(raiz);
			else pai->dir = esquerda(raiz);
		}
		//Se for uma folha.
		else if (esquerda(raiz) == NULL && direita(raiz) == NULL){
			if (pai->esq == raiz) pai->esq = NULL;
			else pai->dir = NULL;
		}
		free(raiz);
	}
}
``` 
