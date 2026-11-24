# Árvore Binária de Busca (BST) em Java

Este repositório contém o código-fonte da minha implementação didática e funcional de uma Árvore Binária de Busca (Binary Search Tree - BST), desenvolvida como projeto individual da disciplina de Estruturas de Dados II.

O projeto usa a abordagem encadeada (cada nó aponta para os filhos), que permite manipular a memória de forma dinâmica.

## 🎬 Vídeo

A explicação teórica, a parte prática e a demonstração do código estão no vídeo do projeto: [assistir no YouTube](https://youtu.be/UKE6F4jH0_M?si=96wslpEsqAeASg_-)

## 🚀 Funcionalidades

A árvore segue a regra da BST: valores menores ficam à esquerda e valores maiores ficam à direita.

1. **Inserção (`insere`):** coloca cada novo valor na posição correta, de forma recursiva.
2. **Impressão em ordem (`imprime`):** percorre Esquerda → Raiz → Direita e mostra os valores em ordem crescente.
3. **Remoção (`remove`):** trata os três casos: nó sem filhos, com 1 filho e com 2 filhos (usando o sucessor).

## 📂 Código-fonte

### `NoArvore.java`

Define o nó da árvore e os métodos recursivos de inserção, impressão e remoção.

```java
public class NoArvore {
    int valor;
    NoArvore esquerda;
    NoArvore direita;

    // Construtor
    public NoArvore(int valor) {
        this.valor = valor;
        this.esquerda = null;
        this.direita = null;
    }

    // Método de Inserção (implementado de forma recursiva)
    public NoArvore insere(NoArvore a, int v) {
        if (a == null) {
            // Se o nó atual for nulo, cria um novo nó (caso base)
            a = new NoArvore(v); 
        } else if (v < a.valor) {
            // Se o valor for menor, insere na subárvore esquerda
            a.esquerda = insere(a.esquerda, v);
        } else {
            // Se o valor for maior ou igual, insere na subárvore direita
            a.direita = insere(a.direita, v);
        }
        return a;
    }
    
    // Método de Impressão (Percurso Em-Ordem)
    // Garante que a saída seja sempre em ordem crescente.
    public void imprime(NoArvore a) {
        if (a != null) {
            // 1. Vai para o nó mais à esquerda
            imprime(a.esquerda);

            // 2. Imprime o valor do nó (a 'Raiz' do momento)
            System.out.print(a.valor + " ");

            // 3. Vai para o nó da direita
            imprime(a.direita);
        }
    }

    // Método auxiliar para buscar o menor elemento da subárvore direita (para a remoção de 2 filhos)
    private NoArvore buscaMenorDireita(NoArvore a) {
        NoArvore atual = a;
        while (atual.esquerda != null) {
            atual = atual.esquerda;
        }
        return atual;
    }

    // Método de Remoção (Tratamento dos 3 Casos)
    public NoArvore remove(NoArvore a, int v) {
        if (a == null) {
            return a; // Não achou
        }

        // Navega pela árvore para encontrar o nó
        if (v < a.valor) {
            a.esquerda = remove(a.esquerda, v);
        } else if (v > a.valor) {
            a.direita = remove(a.direita, v);
        } else {
            // NÓ ENCONTRADO (v == a.valor)

            // Caso 1: Nó Folha ou com 1 Filho (Direita)
            if (a.esquerda == null) {
                return a.direita; // O filho (ou null) assume a posição
            }
            
            // Caso 2: Nó Folha ou com 1 Filho (Esquerda)
            else if (a.direita == null) {
                return a.esquerda; // O filho (ou null) assume a posição
            }

            // Caso 3: Nó com 2 Filhos
            // Encontra o sucessor (menor nó da subárvore direita)
            NoArvore sucessor = buscaMenorDireita(a.direita);

            // Troca o valor do nó atual (a ser removido) pelo valor do sucessor
            a.valor = sucessor.valor;

            // Remove recursivamente o sucessor da subárvore direita
            a.direita = remove(a.direita, sucessor.valor);
        }
        return a;
    }
}
```

### `Principal.java`

Cria a árvore e demonstra a inserção e o percurso em ordem.

```java
public class Principal {
    public static void main(String[] args) {
        // Inicializa a árvore vazia
        NoArvore abb = null; 
        
        // Instância auxiliar para chamar os métodos
        NoArvore operacoes = new NoArvore(0); 
        
        // 1. Sequência de Inserção (exemplo didático: 6 é a raiz)
        abb = operacoes.insere(abb, 6); 
        operacoes.insere(abb, 8);
        operacoes.insere(abb, 4);
        operacoes.insere(abb, 5);
        operacoes.insere(abb, 2);
        operacoes.insere(abb, 3);
        operacoes.insere(abb, 1);
        operacoes.insere(abb, 9);
        operacoes.insere(abb, 7);

        // 2. Demonstração do Percurso Em-Ordem
        System.out.println(">>> Iniciando percurso Em-Ordem (In-Order):");
        operacoes.imprime(abb);
        // Saída esperada: 1 2 3 4 5 6 7 8 9 

        // 3. Exemplo de Remoção (descomente para testar no código)
        // System.out.println("\n\nRemovendo o nó 4...");
        // abb = operacoes.remove(abb, 4);
        // System.out.println("Novo percurso Em-Ordem:");
        // operacoes.imprime(abb);
        // Saída esperada: 1 2 3 5 6 7 8 9 
    }
}
```

## 🛠️ Como executar

1. Crie os arquivos `NoArvore.java` e `Principal.java` com o código acima, na mesma pasta.
2. Compile e rode:

```bash
javac NoArvore.java Principal.java
java Principal
```

Saída esperada:

```
>>> Iniciando percurso Em-Ordem (In-Order):
1 2 3 4 5 6 7 8 9
```

## Autor

**Kayo Victor Vilar Silva**: [LinkedIn](https://www.linkedin.com/in/kayo-victor-vilar-525205373/) · [GitHub](https://github.com/Kay0ox)
