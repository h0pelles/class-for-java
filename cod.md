public class Matrix {
    private int[][] data;
    private int rows;
    private int cols;

    public Matrix(int rows, int cols) {
        this.rows = rows;
        this.cols = cols;
        data = new int[rows][cols];
    }
    public void setValue(int row, int col, int value) {
        data[row][col] = value;
    }
    public int getValue(int row, int col) {
        return data[row][col];
    }
    public static Matrix add(Matrix m1, Matrix m2) {
        if (m1.rows != m2.rows || m1.cols != m2.cols) {
            throw new IllegalArgumentException("Матрицы должны быть одного размера");
        }
        Matrix result = new Matrix(m1.rows, m1.cols);
        for (int i = 0; i < m1.rows; i++) {
            for (int j = 0; j < m1.cols; j++) {
                result.setValue(i, j, m1.getValue(i, j) + m2.getValue(i, j));
            }
        }
        return result;
    }
    public static Matrix subtract(Matrix m1, Matrix m2) {
        if (m1.rows != m2.rows || m1.cols != m2.cols) {
            throw new IllegalArgumentException("Матрицы должны быть одного размера");
        }
        Matrix result = new Matrix(m1.rows, m1.cols);
        for (int i = 0; i < m1.rows; i++) {
            for (int j = 0; j < m1.cols; j++) {
                result.setValue(i, j, m1.getValue(i, j) - m2.getValue(i, j));
            }
        }
        return result;
    }
    public static Matrix multiply(Matrix m1, Matrix m2) {
        if (m1.cols != m2.rows) {
            throw new IllegalArgumentException("Количество столбцов первой матрицы должно совпадать с количеством строк второй матрицы");
        }
        Matrix result = new Matrix(m1.rows, m2.cols);
        for (int i = 0; i < m1.rows; i++) {
            for (int j = 0; j < m2.cols; j++) {
                int sum = 0;
                for (int k = 0; k < m1.cols; k++) {
                    sum += m1.getValue(i, k) * m2.getValue(k, j);
                }
                result.setValue(i, j, sum);
            }
        }
        return result;
    }
    public void print() {
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                System.out.print(data[i][j] + " ");
            }
            System.out.println();
        }
    }
    public static void main(String[] args) {
        Matrix m1 = new Matrix(2, 2);
        m1.setValue(0, 0, 1);
        m1.setValue(0, 1, 2);
        m1.setValue(1, 0, 3);
        m1.setValue(1, 1, 4);

        Matrix m2 = new Matrix(2, 2);
        m2.setValue(0, 0, 5);
        m2.setValue(0, 1, 6);
        m2.setValue(1, 0, 7);
        m2.setValue(1, 1, 8);

        Matrix sum = Matrix.add(m1, m2);
        Matrix diff = Matrix.subtract(m1, m2);
        Matrix product = Matrix.multiply(m1, m2);

        System.out.println("Matrix m1:");
        m1.print();
        System.out.println("Matrix m2:");
        m2.print();
        System.out.println("Sum of m1 and m2:");
        sum.print();
        System.out.println("Difference of m1 and m2:");
        diff.print();
        System.out.println("Product of m1 and m2:");
        product.print();
    }
}
