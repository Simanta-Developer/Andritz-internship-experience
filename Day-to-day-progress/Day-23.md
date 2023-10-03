# :computer: Day-23 :
''' c#
using OfficeOpenXml; // Include the EPPlus namespace

class Program
{
    static void Main(string[] args)
    {
        // Specify the path to your Excel file
        string filePath = "path/to/your/excelfile.xlsx";

        // Load the Excel package
        using (var package = new ExcelPackage(new FileInfo(filePath)))
        {
            // Get the first worksheet in the Excel file
            var worksheet = package.Workbook.Worksheets[0];

            // Determine the number of rows and columns in the worksheet
            int rowCount = worksheet.Dimension.Rows;
            int colCount = worksheet.Dimension.Columns;

            // Iterate through the rows and columns to read data
            for (int row = 1; row <= rowCount; row++)
            {
                for (int col = 1; col <= colCount; col++)
                {
                    // Get the cell value at the current row and column
                    string cellValue = worksheet.Cells[row, col].Value?.ToString();

                    // Process the cell value (you can store it, manipulate it, etc.)
                    Console.WriteLine($"Row: {row}, Column: {col}, Value: {cellValue}");
                }
            }
        }

        Console.WriteLine("Excel data imported successfully!");
    }
}
'''
