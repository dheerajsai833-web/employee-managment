import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import java.awt.*;
import java.awt.event.*;

public class EmployeeManagementForm extends JFrame {
    private JTextField nameField, deptField, salaryField;
    private JButton addButton;
    private JTable employeeTable;
    private DefaultTableModel tableModel;

    public EmployeeManagementForm() {
        setTitle("Employee Management Form");
        setSize(500, 350);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        JPanel inputPanel = new JPanel(new GridLayout(4, 2, 5, 5));
        inputPanel.setBorder(BorderFactory.createTitledBorder("Add Employee"));
        inputPanel.add(new JLabel("Name:"));
        nameField = new JTextField();
        inputPanel.add(nameField);
        inputPanel.add(new JLabel("Department:"));
        deptField = new JTextField();
        inputPanel.add(deptField);
        inputPanel.add(new JLabel("Salary:"));
        salaryField = new JTextField();
        inputPanel.add(salaryField);
        addButton = new JButton("Add Employee");
        inputPanel.add(addButton);
        inputPanel.add(new JLabel(""));

        String[] columns = {"Name", "Department", "Salary"};
        tableModel = new DefaultTableModel(columns, 0);
        employeeTable = new JTable(tableModel);
        JScrollPane tableScroll = new JScrollPane(employeeTable);
        tableScroll.setBorder(BorderFactory.createTitledBorder("Employee List"));

        add(inputPanel, BorderLayout.NORTH);
        add(tableScroll, BorderLayout.CENTER);

        addButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                addEmployee();
            }
        });
    }

    private void addEmployee() {
        String name = nameField.getText().trim();
        String dept = deptField.getText().trim();
        String salaryStr = salaryField.getText().trim();
        if (name.isEmpty() || dept.isEmpty() || salaryStr.isEmpty()) {
            JOptionPane.showMessageDialog(this, "Please fill all fields.");
            return;
        }
        try {
            double salary = Double.parseDouble(salaryStr);
            tableModel.addRow(new Object[]{name, dept, salary});
            nameField.setText("");
            deptField.setText("");
            salaryField.setText("");
        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Salary must be a number.");
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new EmployeeManagementForm().setVisible(true);
            }
        });
    }
}
