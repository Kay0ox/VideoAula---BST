 Árvore Binária de Busca (BST) - Implementação em JavaEste repositório contém o código-fonte da minha implementação didática e funcional de uma Árvore Binária de Busca (Binary Search Tree - BST), desenvolvida como projeto individual da disciplina de Estruturas de Dados II.O projeto foca na abordagem encadeada (ligada), que permite manipulação dinâmica da memória e maior eficiência nas operações.🎬 Assista ao VídeoTodo o conteúdo teórico, prático e a demonstração de execução deste código estão detalhados no meu vídeo oficial do projeto:PlataformaLinkYouTube (Vídeo Completo)Clique para assistir: BST - Do Conceito ao Código Java!👤 Autor e ContatoAutor: KayoGitHub: Kay0oxInstagram: @kay0ox_🚀 Funcionalidades do CódigoO código implementa as operações fundamentais de uma BST, seguindo rigorosamente a regra de organização: valores menores à esquerda, valores maiores à direita.1. 📥 Inserção (insere)Adiciona novos valores na posição correta da árvore de forma recursiva.2. 📄 Impressão Em-Ordem (imprime)O percurso ideal que segue a lógica Esquerda → Raiz → Direita. O resultado prático é a exibição de todos os valores da árvore ordenados de forma crescente.3. ❌ Remoção (remove)Implementação completa da remoção, cobrindo os três casos essenciais (0 filhos, 1 filho, 2 filhos).📂 Código-FonteNoArvore.javaEsta classe define a estrutura básica de cada nó e contém os métodos recursivos que manipulam a árvore (inserção, impressão e remoção).Javapublic class NoArvore {
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
Principal.javaEsta classe é usada apenas para executar o código, criar a árvore e demonstrar a inserção e o percurso Em-Ordem.Javapublic class Principal {
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
🛠️ Como ExecutarClone este repositório.Abra o projeto na sua IDE.Execute o arquivo Principal.java.O console exibirá a sequência de valores inserida de forma desordenada e, em seguida, a saída perfeitamente ordenada pela função imprime, confirmando a organização da BST.
