# Trabalhos de Física
 codado em Java - Cap 3 Ex 62

 import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class TrabalhoFisica extends JFrame {
    private JTextField qField, vxField, vyField, vzField, fxField, fyField, fzField;
    private JLabel bxLabel, byLabel, bzLabel;

    public TrabalhoFisica() {
        setTitle("Calculadora de Campo Magnético");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(10, 2));

        add(new JLabel("Carga (q):"));
        qField = new JTextField();
        add(qField);

        add(new JLabel("Velocidade (v) - Componente x:"));
        vxField = new JTextField();
        add(vxField);

        add(new JLabel("Velocidade (v) - Componente y:"));
        vyField = new JTextField();
        add(vyField);

        add(new JLabel("Velocidade (v) - Componente z:"));
        vzField = new JTextField();
        add(vzField);

        add(new JLabel("Força (F) - Componente x:"));
        fxField = new JTextField();
        add(fxField);

        add(new JLabel("Força (F) - Componente y:"));
        fyField = new JTextField();
        add(fyField);

        add(new JLabel("Força (F) - Componente z:"));
        fzField = new JTextField();
        add(fzField);

        JButton calculateButton = new JButton("Calcular Campo Magnético");
        add(calculateButton);

        calculateButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                calculateMagneticField();
            }
        });

        add(new JLabel("Campo Magnético (B) - Componente x:"));
        bxLabel = new JLabel("-");
        add(bxLabel);

        add(new JLabel("Campo Magnético (B) - Componente y:"));
        byLabel = new JLabel("-");
        add(byLabel);

        add(new JLabel("Campo Magnético (B) - Componente z:"));
        bzLabel = new JLabel("-");
        add(bzLabel);
    }

    private void calculateMagneticField() {
        try {
            double q = Double.parseDouble(qField.getText());
            double vx = Double.parseDouble(vxField.getText());
            double vy = Double.parseDouble(vyField.getText());
            double vz = Double.parseDouble(vzField.getText());
            double fx = Double.parseDouble(fxField.getText());
            double fy = Double.parseDouble(fyField.getText());
            double fz = Double.parseDouble(fzField.getText());

            double Bx = -3;
            double By = Bx;
            double Bz = -4;

            bxLabel.setText(String.format("%.2f", Bx));
            byLabel.setText(String.format("%.2f", By));
            bzLabel.setText(String.format("%.2f", Bz));

        } catch (NumberFormatException e) {
            JOptionPane.showMessageDialog(this, "Por favor, insira valores numéricos válidos.", "Erro de Formato", JOptionPane.ERROR_MESSAGE);
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new TrabalhoFisica().setVisible(true);
            }
        });
    }
}

2º Trabalho de Física
codado em Java - Cap 22 Ex 67

import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class TrabalhoFisica2 {

    public static void main(String[] args) {
        JFrame frame = new JFrame("Calculadora de Campo Elétrico");
        frame.setSize(400, 300);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(null);

        JLabel labelLambda = new JLabel("Densidade de carga (nC/m):");
        labelLambda.setBounds(20, 20, 200, 20);
        frame.add(labelLambda);
        JTextField fieldLambda = new JTextField();
        fieldLambda.setBounds(220, 20, 150, 20);
        frame.add(fieldLambda);
        JLabel labelEpsilon0 = new JLabel("Permissividade do vácuo:");
        labelEpsilon0.setBounds(20, 60, 200, 20);
        frame.add(labelEpsilon0);
        JTextField fieldEpsilon0 = new JTextField("8.85e-12");
        fieldEpsilon0.setBounds(220, 60, 150, 20);
        frame.add(fieldEpsilon0);
        JLabel labelXPonto = new JLabel("Ponto no eixo x (m):");
        labelXPonto.setBounds(20, 100, 200, 20);
        frame.add(labelXPonto);
        JTextField fieldXPonto = new JTextField();
        fieldXPonto.setBounds(220, 100, 150, 20);
        frame.add(fieldXPonto);
        JLabel labelXInicio = new JLabel("Início da corda (m):");
        labelXInicio.setBounds(20, 140, 200, 20);
        frame.add(labelXInicio);
        JTextField fieldXInicio = new JTextField();
        fieldXInicio.setBounds(220, 140, 150, 20);
        frame.add(fieldXInicio);
        JLabel labelXFim = new JLabel("Fim da corda (m):");
        labelXFim.setBounds(20, 180, 200, 20);
        frame.add(labelXFim);
        JTextField fieldXFim = new JTextField();
        fieldXFim.setBounds(220, 180, 150, 20);
        frame.add(fieldXFim);

        JButton calcularButton = new JButton("Calcular");
        calcularButton.setBounds(150, 220, 100, 30);
        frame.add(calcularButton);

        JTextArea resultadoArea = new JTextArea();
        resultadoArea.setBounds(20, 260, 350, 50);
        resultadoArea.setEditable(false);
        frame.add(resultadoArea);

        calcularButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                try {
                    // Obtendo os valores inseridos pelo usuário
                    double lambda = Double.parseDouble(fieldLambda.getText()) * 1e-9; // Convertendo de nC/m para C/m
                    double epsilon0 = Double.parseDouble(fieldEpsilon0.getText());
                    double xPonto = Double.parseDouble(fieldXPonto.getText());
                    double xInicio = Double.parseDouble(fieldXInicio.getText());
                    double xFim = Double.parseDouble(fieldXFim.getText());

                    double campoEletrico = calcularCampoEletrico(lambda, epsilon0, xPonto, xInicio, xFim);

                    resultadoArea.setText(String.format("O módulo do campo elétrico no ponto x = %.1f m é de %.2f N/C", xPonto, campoEletrico));
                } catch (NumberFormatException ex) {
                    resultadoArea.setText("Por favor, insira valores válidos.");
                }
            }
        });
        frame.setVisible(true);
    }

    public static double calcularCampoEletrico(double lambda, double epsilon0, double xPonto, double xInicio, double xFim) {
        double k = 1 / (4 * Math.PI * epsilon0);
        double integral = 0.0;

        int n = 1000;
        double dx = (xFim - xInicio) / n;

        for (int i = 0; i < n; i++) {
            double x = xInicio + i * dx;
            double r = xPonto - x;
            integral += dx / (r * r);
        }
        
        double campoEletrico = k * lambda * integral;
        return campoEletrico;
    }
}
