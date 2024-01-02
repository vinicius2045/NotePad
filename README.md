package com.mycompany.notepadalgii;

import javax.swing.JFileChooser;
import javax.swing.JFrame;
import javax.swing.JMenu;
import javax.swing.JMenuBar;
import javax.swing.JMenuItem;
import javax.swing.JOptionPane;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import java.awt.BorderLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;

public class NotepadAlgII extends JFrame implements ActionListener {
    private JTextArea textArea;

    public NotepadAlgII() {
        setTitle("Notepad");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(500, 500);

        JMenuBar menuBar = new JMenuBar();
        setJMenuBar(menuBar);

        JMenu fileMenu = new JMenu("Arquivo");
        JMenu editMenu = new JMenu("Editar");
        JMenu helpMenu = new JMenu("Ajuda");

        JMenuItem newMenuItem = new JMenuItem("Novo");
        JMenuItem openMenuItem = new JMenuItem("Abrir");
        JMenuItem saveMenuItem = new JMenuItem("Salvar");
        JMenuItem exitMenuItem = new JMenuItem("Sair");

        JMenuItem cutMenuItem = new JMenuItem("Cortar");
        JMenuItem copyMenuItem = new JMenuItem("Copiar");
        JMenuItem pasteMenuItem = new JMenuItem("Colar");
        JMenuItem selectAllMenuItem = new JMenuItem("Selecionar Tudo");

        JMenuItem aboutMenuItem = new JMenuItem("Sobre");

        fileMenu.add(newMenuItem);
        fileMenu.add(openMenuItem);
        fileMenu.add(saveMenuItem);
        fileMenu.add(exitMenuItem);

        editMenu.add(cutMenuItem);
        editMenu.add(copyMenuItem);
        editMenu.add(pasteMenuItem);
        editMenu.add(selectAllMenuItem);

        helpMenu.add(aboutMenuItem);

        menuBar.add(fileMenu);
        menuBar.add(editMenu);
        menuBar.add(helpMenu);

        newMenuItem.addActionListener(this);
        openMenuItem.addActionListener(this);
        saveMenuItem.addActionListener(this);
        exitMenuItem.addActionListener(this);

        cutMenuItem.addActionListener(this);
        copyMenuItem.addActionListener(this);
        pasteMenuItem.addActionListener(this);
        selectAllMenuItem.addActionListener(this);

        aboutMenuItem.addActionListener(this);

        textArea = new JTextArea();
        JScrollPane scrollPane = new JScrollPane(textArea);
        add(scrollPane, BorderLayout.CENTER);

        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        String command = e.getActionCommand();

        if (command.equals("Sair")) {
            System.exit(0);
        } else if (command.equals("Sobre")) {
            exibirDialogoSobre();
        } else if (command.equals("Novo")) {
            novoDocumento();
        } else if (command.equals("Abrir")) {
            abrirDocumento();
        } else if (command.equals("Salvar")) {
            salvarDocumento();
        } else if (command.equals("Cortar")) {
            cortarTexto();
        } else if (command.equals("Copiar")) {
            copiarTexto();
        } else if (command.equals("Colar")) {
            colarTexto();
        } else if (command.equals("Selecionar Tudo")) {
            selecionarTodoTexto();
        }
    }

    private void exibirDialogoSobre() {
        JOptionPane.showMessageDialog(this, "Vinicius vieira", "Sobre", JOptionPane.INFORMATION_MESSAGE);
    }

    private void novoDocumento() {
        textArea.setText("");
    }

    private void abrirDocumento() {
    JFileChooser fileChooser = new JFileChooser();
    int result = fileChooser.showOpenDialog(this);
    if (result == JFileChooser.APPROVE_OPTION) {
        File file = fileChooser.getSelectedFile();
        try {
            BufferedReader reader = new BufferedReader(new FileReader(file));
            textArea.read(reader, null);
            reader.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

private void salvarDocumento() {
    JFileChooser fileChooser = new JFileChooser();
    int result = fileChooser.showSaveDialog(this);
    if (result == JFileChooser.APPROVE_OPTION) {
        File file = fileChooser.getSelectedFile();
        try {
            BufferedWriter writer = new BufferedWriter(new FileWriter(file));
            textArea.write(writer);
            writer.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
private void cortarTexto() {
    textArea.cut();
}

private void copiarTexto() {
    textArea.copy();
}

private void colarTexto() {
    textArea.paste();
}

private void selecionarTodoTexto() {
    textArea.selectAll();
}
    
    

    public static void main(String[] args) {
        new NotepadAlgII();
    }
}
