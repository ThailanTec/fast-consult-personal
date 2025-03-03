# Matriz

Matriz é uma estrutura de dados que armazena uma coleção de elementos do mesmo tipo, organizado por linhas e colunas. 

**Como funciona?** 

- **Organização:**
    - Os elementos são acessados por meio de indices, que indicam a posiução da linha e da cluna.
    - Em Go, como muitas linguagens, os indices começam em 0.
- **Declaração:**
    - Para criar uma matriz em GO, você precisa especificar o tipo dos elementos e o tamanho das linhas e colunas.
    
    ```go
    var matriz [3][3]int
    ```
    
- **Uso:**
    - Matrizes são úteis para repsentar dados tabulares, como planilhas, imagens (pixels) ou jogos (tabuleiros)

**Exemplos em Go:**

```go

package main

import "fmt"

func main() {

	// Declara uma matriz 3x3 de inteiros
	var matriz [3][3]int

	matriz[0][0] = 1
	matriz[0][1] = 2
	matriz[0][2] = 3
	matriz[1][0] = 4
	matriz[1][1] = 5
	matriz[1][2] = 6
	matriz[2][0] = 7
	matriz[2][1] = 8
	matriz[2][2] = 9

	fmt.Println(matriz)

	for i := 0; i < 3; i++ {
		for j := 0; j < 3; j++ {
			fmt.Println("Os dados da matriz: ", matriz[i][j])
		}
	}
}

```