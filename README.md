#include <iostream>
#include <fstream>
#include <string>
#include <algorithm>

using namespace std;

const string kNomeArquivoBancoDeDados = "db.txt";

void PaginaInicial();

void LimparTela() {
    cout << string( 100, '\n' );
}

void MostrarTodosOsProdutos() {
    int total_produtos = 0;
    std::string nome, tamanho, quantidade, line_;

    ifstream file(kNomeArquivoBancoDeDados);

    if (file.is_open()) {
        while (getline(file, line_)) {
            cout << line_ << "\n";
            total_produtos++;
        }
        file.close();
    }

    int acao;

    while (true) {
        cout << "\n \n";
        cout << "Total de Produtos: " << total_produtos << "\n";
        cout << "Digite 0 para voltar ao menu anterior: ";
        cin >> acao;

        if (acao == 0) {
            PaginaInicial();
            break;
        } else {
            LimparTela();
            MostrarTodosOsProdutos();
            break;
        }
    }
}

void ProcurarProdutoID() {
    int id_inserido, id;
    std::string nome, tamanho, quantidade, line_,valor;

    ifstream file;
    file.open(kNomeArquivoBancoDeDados);

    cout << "Digite o ID do produto: ";
    cin >> id_inserido;

    LimparTela();

    cout << "Resultados para o ID:" << id_inserido << "\n \n";

    if (file.is_open()) {
        while (file >> id >> nome >> valor >> tamanho >> quantidade) {
            if (id == id_inserido) {
                cout << id << " " << nome << " " << valor << " " << " " << tamanho << " " << quantidade;
            }
        }
        file.close();
    }

    int acao;

    while (true) {
        cout << "\n \n";
        cout << "Digite 0 para voltar ao menu anterior ou 1 para buscar \n";
        cin >> acao;

        if (acao == 1) {
            LimparTela();
            ProcurarProdutoID();
            break;
        } else if (acao == 0) {
            PaginaInicial();
            break;
        }
        cout << "Opção inválida, por favor tente novamente \n";
    }
}

void ProcurarProdutoPorNome() {
    std::string nome_produto, nome, tamanho, quantidade;
    int id, valor;

    ifstream file;

    file.open(kNomeArquivoBancoDeDados);

    cout << "Digite o nome do produto: ";
    cin >> nome_produto;

    LimparTela();

    cout << "Resultados para o nome: " << nome_produto << "\n \n";

    if (file.is_open()) {
        while (file >> id >> nome >> valor >> tamanho >> quantidade) {
            if (nome == nome_produto) {
                cout << id << " " << nome << " " << valor << " " << " " << tamanho << " " << quantidade;
            }
        }
        file.close();
    }

    int acao;

    while (true) {
        cout << "\n \n";
        cout << "Digite 0 para voltar ao menu anterior ou 1 para buscar \n";
        cin >> acao;

        if (acao == 1) {
            LimparTela();
            ProcurarProdutoPorNome();
            break;
        }

        if (acao == 0) {
            PaginaInicial();
            break;
        }

        LimparTela();
        ProcurarProdutoPorNome();
        break;
    }
}

void ProcurarProdutoPorTamanho() {
    int id, valor;
    std::string tamanho_produto, nome, tamanho, quantidade, line_;

    ifstream file(kNomeArquivoBancoDeDados);

    cout << "Digite o tamanho do produto: ";
    cin >> tamanho_produto;

    LimparTela();

    cout << "Resultados por tamanho:" << tamanho_produto << "\n \n";

    if (file.is_open()) {
        while (file >> id >> nome >> valor >> tamanho >> quantidade) {
            if (tamanho == tamanho_produto) {
                cout << id << " " << nome << " " << valor << " " << tamanho << " " << quantidade << "\n";
            }
        }
        file.close();
    }

    int acao;

    while (true) {
        cout << "\n \n";
        cout << "Digite 0 para voltar ao menu anterior ou 1 para buscar \n";
        cin >> acao;

        if (acao == 1) {
            LimparTela();
            ProcurarProdutoPorTamanho();
            break;
        }

        if (acao == 0) {
            PaginaInicial();
            break;
        }

        LimparTela();
        ProcurarProdutoPorTamanho();
        break;
    }
}

void BuscarProdutoPorValor() {
    int total_produtos = 0;
    int id,valor_inserido, quantidade, valor;
    std::string nome, tamanho, line_;

    ifstream file(kNomeArquivoBancoDeDados);

    cout << "Digite o valor do produto: ";
    cin >> valor_inserido;

    LimparTela();

    cout << "Resultados por valor:" << valor_inserido << "\n \n";

    if (file.is_open()) {
        while (file >> id >> nome >> valor >> tamanho >> quantidade) {
            if (valor == valor_inserido) {
                cout << id << " " << nome << " " << valor << " " << tamanho << " " << quantidade << "\n";
                total_produtos++;
            }
        }
        file.close();
    }

    int acao;

    while (true) {
        cout << "\n \n";
        cout << "Total de Produtos: " << total_produtos << "\n";
        cout << "Digite 0 para voltar ao menu anterior ou 1 para Buscar \n";
        cin >> acao;

        if (acao == 1) {
            LimparTela();
            BuscarProdutoPorValor();
            break;
        } else if (acao == 0) {
            PaginaInicial();
            break;
        }
        cout << "Ação inválida, por favor tente novamente \n";
    }
}

int CalcularProximoId() {
    int id = 1;

    std::string line_;
    ifstream file(kNomeArquivoBancoDeDados);

    if (file.is_open()) {
        while (getline(file, line_)) {
            cout << line_ << "\n";
            id++;
        }
        file.close();
    }
    return id;
}

void InserirProduto() {
    std::string line_, nome, tamanho;
    int quantidade, valor;
    int id = CalcularProximoId();

    ifstream file;
    file.open(kNomeArquivoBancoDeDados);

    ofstream arquivo;
    arquivo.open(kNomeArquivoBancoDeDados, ios::app);

    cout << "\n\nDigite o nome do produto: ";
    cin >> nome;

    cout << "Digite o valor do produto: ";
    cin >> valor;

    cout << "Digite o tamanho do produto: ";
    cin >> tamanho;

    cout << "Digite a quantidade do produto: ";
    cin >> quantidade;

    cin.ignore();

    if (file.is_open()) {
        arquivo << id << " " << nome << " " << valor << " " << tamanho << " " << quantidade << "\n";
        arquivo.close();
        file.close();
    }

    cout << "\n\n";
    cout << "Produto cadastrado com sucesso! \n";

    int acao;

    while (true) {
        cout << "Digite 0 para voltar ao menu anterior ou 1 para cadastrar \n";
        cin >> acao;

        LimparTela();

        if (acao == 0) {
            PaginaInicial();
            break;
        } else if (acao == 1) {
            InserirProduto();
            break;
        }
        cout << "Ação inválida, por favor tente novamente \n";
    }
}

int PegarTamanhoDoBancoDeDados() {
    int length = 0;

    std::string line_;

    ifstream file;
    file.open(kNomeArquivoBancoDeDados);

    if (file.is_open()) {
        while (getline(file, line_)) {
            length++;
        }
        file.close();
    }
    return length;
}

void RemoverProduto() {
    int id_produto, id, valor, quantidade;
    int line_id = 0;
    int tamanho_banco = PegarTamanhoDoBancoDeDados();

    std::string nome, tamanho, line_;
    std::string lines[tamanho_banco - 1];

    cout << "Digite o ID que deseja remover: ";
    cin >> id_produto;

    ifstream file;
    file.open(kNomeArquivoBancoDeDados);

    if (file.is_open()) {
        while (file >> id >> nome >> valor >> tamanho >> quantidade) {
            if (id != id_produto) {
                lines[line_id] = to_string(id) +  " " + nome + " " + to_string(valor) + " " + tamanho + " " + to_string(quantidade) + "\n";
                line_id++;
            }
        }
        file.close();
    }

    int index = 0;
    ofstream arq;
    arq.open(kNomeArquivoBancoDeDados);

    if (arq.is_open()) {
        while (index < tamanho_banco - 1) {
            arq << lines[index];
            cout << lines[index];
            index++;
        }
        arq.close();
    }

    cout << "Produto com ID " << id_produto << " removido com sucesso!";

    int acao;

    while (true) {
        cout << "\n \n";
        cout << "Digite 0 para voltar ao menu anterior ou 1 para deletar \n";
        cin >> acao;

        if (acao == 1) {
            RemoverProduto();
            break;
        } else if (acao == 0) {
            PaginaInicial();
            break;
        } else {
            cout << "Ação inválida, por favor tente novamente \n";
        }
    }
}

void AlterarProduto() {
    int tamanho_banco = PegarTamanhoDoBancoDeDados();
    bool exist_id = false;
    int line_id = 0;
    int linha_id_produto, id_produto, id;

    std::string lines[tamanho_banco];
    std::string nome, valor, tamanho, quantidade;

    cout << "Digite o ID que deseja modificar: ";
    cin >> id_produto;

    ifstream file;
    file.open(kNomeArquivoBancoDeDados);

    if (file.is_open()) {
        while ( file >> id >> nome >> valor >> tamanho >> quantidade ) {
            if (id == id_produto) {
                exist_id = true;
                linha_id_produto = line_id;
            }
            lines[line_id] = to_string(id) +  " " + nome + " " + valor + " " + tamanho + " " + quantidade + "\n";
            line_id++;
        }
        file.close();
    }

    if (exist_id) {
        std::string novo_nome, novo_valor, novo_tamanho, nova_quantidade;

        cout << "Editar nome do produto: ";
        cin >> novo_nome;

        cout << "Editar valor do produto: ";
        cin >> novo_valor;

        cout << "Editar tamanho do produto: ";
        cin >> novo_tamanho;

        cout << "Editar quantidade do produto: ";
        cin >> nova_quantidade;

        ofstream arq;
        arq.open(kNomeArquivoBancoDeDados);

        int index = 0;

        if (arq.is_open()) {
            while (index < tamanho_banco) {
                if (index == linha_id_produto) {
                    arq << id_produto << " " << novo_nome << " " << novo_valor << " " << novo_tamanho << " " << nova_quantidade << "\n";
                } else {
                    arq << lines[index];
                }
                index++;
            }
            arq.close();
        }

        int acao;

        while (true) {
            cout << "\n \n";
            cout << "Digite 0 para voltar ao menu anterior ou 1 para editar \n";
            cin >> acao;

            if (acao == 1) {
                LimparTela();
                AlterarProduto();
                break;
            } else if (acao == 0) {
                LimparTela();
                PaginaInicial();
                break;
            }
            cout << "Ação inválida, por favor tente novamente \n";
        }
    } else {
        int acao;

        cout << "ID inexiste! \n";

        while (true) {
            cout << "\n \n";
            cout << "Digite 0 para voltar ao menu anterior \n";
            cin >> acao;

            if (acao == 0) {
                LimparTela();
                PaginaInicial();
                break;
            }
            cout << "Ação inválida, por favor tente novamente \n";
        }
    }

}

void MostrarMenu() {
    cout << "======= PROGRAMA PARA CONTROLE DE PRODUTOS =======\n";
    cout << "Selecione uma opcao: \n \n";
    cout << "1 - Listar Todos os Produtos \n";
    cout << "2 - Procurar Cadastro(s) por ID \n";
    cout << "3 - Procurar Cadastro(s) por nome \n";
    cout << "4 - Procurar Cadastro(s) por tamanho \n";
    cout << "5 - Procurar Cadastro(s) por valor \n";
    cout << "6 - Cadastrar um produto no banco de dados \n";
    cout << "7 - Remover um produto no banco de dados \n";
    cout << "8 - Editar um produto no banco de dados \n";
}

void PaginaInicial() {
    int opcao;

    LimparTela();
    MostrarMenu();

    cin >> opcao;

    LimparTela();

    switch (opcao) {
        case 1:
            MostrarTodosOsProdutos(); // OK
            break;
        case 2:
            ProcurarProdutoID(); // OK
            break;
        case 3:
            ProcurarProdutoPorNome(); // OK
            break;
        case 4:
            ProcurarProdutoPorTamanho(); // OK
            break;
        case 5:
            BuscarProdutoPorValor(); // OK
            break;
        case 6:
            InserirProduto(); // OK
            break;
        case 7:
            RemoverProduto(); // flag
            break;
        case 8:
            AlterarProduto(); // ok
            break;
    }
}

int main() {
    PaginaInicial();
    return 0;
}
