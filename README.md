package Trabalho_final;

import java.util.Scanner;

public class ListaTarefas {

    public static final String RESET = "\u001B[0m";
    public static final String GREEN = "\u001B[32m";
    public static final String YELLOW = "\u001B[33m";
    public static final String RED = "\u001B[31m";

    public static void adicionarTarefa(String[][] matriz, int linhas) {
        Scanner scanner = new Scanner(System.in);
        int linha = -1;

        for (int i = 0; i < linhas; i++) {
            if (matriz[i][0] == null) {
                linha = i;
                break;
            }
        }

        if (linha != -1) {
            System.out.println("Insira o nome da tarefa: ");
            matriz[linha][0] = scanner.nextLine();
            System.out.println("Insira a descrição da tarefa: ");
            matriz[linha][1] = scanner.nextLine();
            System.out.println("Insira o seu nome: ");
            matriz[linha][2] = scanner.nextLine();
            System.out.println("Insira o horário da tarefa: ");
            matriz[linha][3] = scanner.nextLine();
            matriz[linha][4] = "Em espera";

            System.out.println("Tarefa adicionada.");
        } else {
            System.out.println("A lista de tarefas está cheia.");
        }
    }

    public static void mostrarTarefas(String[][] matriz, int linhas) {
        System.out.println("Lista de Tarefas:");
        for (int i = 0; i < linhas; i++) {
            if (matriz[i][0] != null) {
                System.out.print((i + 1) + " - Nome: " + matriz[i][0]);
                System.out.print("   Descrição: " + matriz[i][1]);
                System.out.print("   Nome do usuário: " + matriz[i][2]);
                System.out.print("   Horário da tarefa: " + matriz[i][3]);
                String status = matriz[i][4];
                if (status.equals("Concluída")) {
                    System.out.print("   Status: " + GREEN + status + RESET);
                } else if (status.equals("Em espera")) {
                    System.out.print("   Status: " + YELLOW + status + RESET);
                } else if (status.equals("Não feita")) {
                    System.out.print("   Status: " + RED + status + RESET);
                }
                System.out.println();
            }
        }
    }

    public static void marcarTarefaConcluida(String[][] matriz, int linhas) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Informe o número da tarefa que deseja marcar como concluída: ");
        int numeroTarefa = scanner.nextInt();

        if (numeroTarefa >= 1 && numeroTarefa <= linhas) {
            int indiceTarefa = numeroTarefa - 1;
            if (matriz[indiceTarefa][0] != null) {
                matriz[indiceTarefa][4] = "Concluída";
                System.out.println("Tarefa marcada como concluída.");
            } else {
                System.out.println("Tarefa não encontrada.");
            }
        } else {
            System.out.println("Número de tarefa inválido.");
        }
    }

    public static void marcarTarefaNaoFeita(String[][] matriz, int linhas) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Informe o número da tarefa que deseja marcar como não feita: ");
        int numeroTarefa = scanner.nextInt();

        if (numeroTarefa >= 1 && numeroTarefa <= linhas) {
            int indiceTarefa = numeroTarefa - 1;
            if (matriz[indiceTarefa][0] != null) {
                matriz[indiceTarefa][4] = "Não feita";
                System.out.println("Tarefa marcada como não feita.");
            } else {
                System.out.println("Tarefa não encontrada.");
            }
        } else {
            System.out.println("Número de tarefa inválido.");
        }
    }

    public static void removerTarefa(String[][] matriz, int linhas) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Informe o número da tarefa que deseja remover: ");
        int numeroTarefa = scanner.nextInt();

        if (numeroTarefa >= 1 && numeroTarefa <= linhas) {
            int indiceTarefa = numeroTarefa - 1;
            if (matriz[indiceTarefa][0] != null) {
                matriz[indiceTarefa][0] = null;
                matriz[indiceTarefa][1] = null;
                matriz[indiceTarefa][2] = null;
                matriz[indiceTarefa][3] = null;
                matriz[indiceTarefa][4] = null;
                System.out.println("Tarefa removida.");
            } else {
                System.out.println("Tarefa não encontrada.");
            }
        } else {
            System.out.println("Número de tarefa inválido.");
        }
    }

    public static void main(String[] args) {
        int tarefas = 5;
        String[][] lista = new String[tarefas][5];
        int opcao;

        Scanner scanner = new Scanner(System.in);

        do {
            System.out.println("Escolha uma opção: \n 1 - Mostrar lista de tarefas. \n 2 - Adicionar tarefa. \n 3 - Marcar tarefa como concluída. \n 4 - Marcar tarefa como não feita. \n 5 - Remover tarefa. \n 0 - Sair.");
            opcao = scanner.nextInt();

            switch (opcao) {
                case 0:
                    break;
                case 1:
                    mostrarTarefas(lista, tarefas);
                    break;
                case 2:
                    adicionarTarefa(lista, tarefas);
                    break;
                case 3:
                    marcarTarefaConcluida(lista, tarefas);
                    break;
                case 4:
                    marcarTarefaNaoFeita(lista, tarefas);
                    break;
                case 5:
                    removerTarefa(lista, tarefas);
                    break;
                default:
                    System.out.println("Opção inválida!");
            }
        } while (opcao != 0);
    }
}
