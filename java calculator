
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Calculator extends JFrame implements ActionListener {

    private final JTextField display;
    private String current = "";
    private String operator = "";
    private double firstValue = 0;
    private boolean startNew = true;

    public Calculator() {
        setTitle("Calculator");
        setSize(320, 420);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setLayout(new BorderLayout());

        display = new JTextField("0");
        display.setHorizontalAlignment(SwingConstants.RIGHT);
        display.setEditable(false);
        display.setFont(new Font("Arial", Font.BOLD, 28));
        add(display, BorderLayout.NORTH);

        JPanel buttons = new JPanel();
        buttons.setLayout(new GridLayout(5, 4, 5, 5));

        String[] labels = {
            "CE", "C", "<-", "/",
            "7", "8", "9", "*",
            "4", "5", "6", "-",
            "1", "2", "3", "+",
            "+/-", "0", ".", "="
        };

        for (String lbl : labels) {
            JButton btn = new JButton(lbl);
            btn.setFont(new Font("Arial", Font.PLAIN, 20));
            btn.addActionListener(this);
            buttons.add(btn);
        }

        add(buttons, BorderLayout.CENTER);
        setVisible(true);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new Calculator());
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        String cmd = e.getActionCommand();

        if (cmd.matches("[0-9]") || cmd.equals(".")) {
            if (startNew) {
                current = cmd.equals(".") ? "0." : cmd;
                startNew = false;
            } else {
                if (cmd.equals(".") && current.contains(".")) {
                    return;
                }
                current += cmd;
            }
            display.setText(current);
            return;
        }

        switch (cmd) {
            case "C":
                current = "";
                operator = "";
                firstValue = 0;
                display.setText("0");
                startNew = true;
                break;
            case "CE":
                current = "";
                display.setText("0");
                startNew = true;
                break;
            case "<-":
                if (!startNew && current.length() > 0) {
                    current = current.substring(0, current.length() - 1);
                    if (current.equals("")) {
                        display.setText("0");
                    } else {
                        display.setText(current);
                    }
                }
                break;
            case "+/-":
                if (!startNew && !current.equals("")) {
                    if (current.startsWith("-")) {
                        current = current.substring(1);
                    } else {
                        current = "-" + current;
                    }
                    display.setText(current);
                }
                break;
            case "+":
            case "-":
            case "*":
            case "/":
                computeOperator(cmd);
                break;
            case "=":
                computeResult();
                operator = "";
                break;
            default:
                break;
        }
    }

    private void computeOperator(String op) {
        try {
            if (!operator.equals("")) {
                computeResult();
            } else if (!current.equals("")) {
                firstValue = Double.parseDouble(current);
            }
        } catch (NumberFormatException ex) {
            display.setText("Error");
            current = "";
            startNew = true;
            return;
        }
        operator = op;
        startNew = true;
    }

    private void computeResult() {
        if (operator.equals("") || current.equals("")) {
            return;
        }
        try {
            double second = Double.parseDouble(current);
            double result = 0;
            switch (operator) {
                case "+":
                    result = firstValue + second;
                    break;
                case "-":
                    result = firstValue - second;
                    break;
                case "*":
                    result = firstValue * second;
                    break;
                case "/":
                    if (second == 0) {
                        display.setText("Cannot divide by zero");
                        current = "";
                        startNew = true;
                        operator = "";
                        return;
                    }
                    result = firstValue / second;
                    break;
            }
            String out = (result == (long) result) ? String.format("%d", (long) result) : String.valueOf(result);
            display.setText(out);
            current = out;
            firstValue = result;
            startNew = true;
        } catch (NumberFormatException ex) {
            display.setText("Error");
            current = "";
            startNew = true;
        }
    }
}

