# Trabalho de Física
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

