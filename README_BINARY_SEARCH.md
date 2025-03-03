# Algoritmos Com GO

## **Pesquisa Binária**

Utilizamos para fazer buscar em **listas Ordenadas**. O Algoritmos vai fazer sempre fazer o seguinte:
Ir no meio da lista e vê se o valor que informamos é maior ou menor do que o valor de informamos. 
Exemplo:

A lista tem 5 casas. *(Lembrando, que começa a conta do 0 na programação, então, seriam 4)*

**[ 3,5,6,9,12]**

 O nosso usuário digitou que busca o numero 9, o nosso algoritmo, vai buscar primeiro no meio da tabela. Caso o numero do meio da tabela seja menor que 9, ele vai cortar todos os números anteriores ao meio, pois já se sabe que o as casas atrás são menores e logo, não faz sentido continuar a busca dessa forma. Logo em seguida, ele busca novamente, buscando assimilando o meio da tabela, ao numero que faltaram: 

[…**9,12],** batendo então, no numero 9. E então, dando o resultado da busca, com apenas 2 tentativas, fazendo assim com que a busca tenha uma rápida velocidade de execução. 

***Exemplo do código em GO:***

```go
import "fmt"

func main() {

	list := []int{2, 4, 6, 8, 10, 13, 15}

	position := binarySearch(list, 13)

	fmt.Println(position)
}

func binarySearch(list []int, numeroQuerido int) int {

	baixo := 0
	alto := len(list) - 1

	for baixo <= alto {
		middle := (alto + baixo) / 2
		chute := list[middle]

		if chute == numeroQuerido {
			return middle
		}

		if chute > numeroQuerido {
			alto = middle - 1
		}

		if chute < numeroQuerido {
			baixo = middle + 1
		}
	}

	return -1
}

/*
Resposta do exercicio:

1 - log 128 == 7 ~ 2^7 == 128
2 - log 256 == 8 ~ 2^8 == 256

*/
```

Go Extras: 

```go
len(list)
```

> use the len built-in function to get string lengths. Len supports arrays, slices and maps.
> 

> `use a função interna len para obter comprimentos de string. Len suporta matrizes, fatias e mapas.`
> 

### Recapitulando

- A pesquisa binária é muito mais rápida do que a pesquisa simples.
- O(Log n) é mais rápido do que O(n), e O(log n) fica ainda mais rápido conforme os elementos da lista aumentam.
- A rapidez de um algoritmo não é medida em segundos.
- O tempo de execução de um algoritmo é medido por meio de seu crescimento.
- O tempo de execução dos algoritmos é expresso na notação Big O.

### Array´s & Listas

Tempo de execução de para operações comuns de **array** e **listas**. 

|  | **Array**   | **Listas** |
| --- | --- | --- |
| **Leitura** |  O(1) |  O(n) |
| **Escrita**  | O(n) |  O(1) |

Tempo de execução para as operações mais comuns em **array** e **listas** encadeadas. 

|  | **Array** | **Listas** |
| --- | --- | --- |
|  **Leitura** | O(1) | O(n) |
| **Inserção** | O(n) | O(1) |
| **Eliminação** | O(n) | O(1) |

> ***Obs.: Para que inserções e eliminações terão tempo de execução O(1) somente se você puder acessar instantaneamente o elemento a ser deletado. É uma pratica comum acompanhar o primeiro e o ultimo item de uma lista encadeada para que o tempo de execução para deletá-los seja O(1).***
> 

**Tipos de acessos**

**Aleatório**

Permite que você pule direto para o elemento desejado. Muitos casos requerem o acesso aleatório, o que faz com que arrays serem mais utilizados. 

**Sequencial**

Significa ler os elementos, um por um, começando pelo primeiro. Listas encadeadas só podem lidar com o acesso sequencial. 

### Recapitulando

- A memória do seu computador é como um conjunto gigante de gavetas
- Quando se quer armazenar múltiplos elementos, usa-se um array ou uma lista.
- No array, todos os elementos são armazenados um ao lado do outro.
- Na lista, os elementos estão espalhados e um elemento armazena o endereço no próximo elemento.
- Arrays permitem leituras rápidas.
- Listas encadeadas permitem rápidas inserções e eliminações.
- Todos os elementos de um array devem ser do mesmo tipo (todos int., strings, bools, etc.)

[Notação BigO ](https://www.notion.so/Nota-o-BigO-1a6c7724d6f3809e811fca166ded6a0a?pvs=21)

[Array & Slice](https://www.notion.so/Array-Slice-1a6c7724d6f380c1a926c6c60ebc3201?pvs=21)

[Circular Buffer](https://www.notion.so/Circular-Buffer-1abc7724d6f3806db6f9f2328a04b185?pvs=21)

[Matriz](https://www.notion.so/Matriz-1abc7724d6f3808499fcd0dd73933df4?pvs=21)