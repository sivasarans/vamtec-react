```markdown
# vamtec-react

`vamtec-react` is a React utility library designed to simplify common frontend tasks, such as file downloading, handling different file formats, and more.

## Installation

To install the library, you can use either `npm` or `yarn`:

### npm:
```bash
npm install vamtec-react
```

### yarn:
```bash
yarn add vamtec-react
```

## Usage

### Downloading Files

The library provides a simple utility for triggering file downloads from a given data source.

```js
import { DownloadFile } from 'vamtec-react';

const handleDownload = (data, fileName, fileExtension) => {
  DownloadFile(fileName, fileExtension, data);
};
```

### Example: Downloading Leave Requests

Here’s an example using `axios` to download leave requests in different formats such as Excel, CSV, or PDF.

```js
import React, { useState } from 'react';
import axios from 'axios';
import { DownloadFile } from 'vamtec-react';

const App = () => {
  const [fileFormat, setFileFormat] = useState("excel"); // Default to 'excel' without the dot

  const handleDownload = async () => {
    try {
      const response = await axios.get(`http://localhost:5000/download-leave-requests?format=${fileFormat}`, { responseType: 'blob' });
      // Map 'excel', 'csv', 'pdf' to their respective extensions
      const fileExtension = fileFormat === "excel" ? ".xlsx" : fileFormat === "csv" ? ".csv" : ".pdf";
      // Call the fileHandling function with correct file name and extension
      DownloadFile('Download', fileExtension, response.data); // Pass base filename, extension, and data
    } catch (error) {
      console.error('Error downloading file', error);
    }
  };

  return (
    <div>
      <h1 className="text-2xl font-bold mb-4">Download Leave Requests</h1>
      <select value={fileFormat} onChange={(e) => setFileFormat(e.target.value)} className="p-2 border rounded-md w-full mb-4">
        <option value="excel">Excel (.xlsx)</option>
        <option value="csv">CSV (.csv)</option>
        <option value="pdf">PDF (.pdf)</option>
      </select>
      <button onClick={handleDownload} className="bg-blue-500 text-white p-2 rounded mt-4">
        Download Leave Requests
      </button>
    </div>
  );
};

export default App;
```

### API

#### `DownloadFile(baseFilename, fileExtension, data)`

- **baseFilename** (`string`): The base name of the file (without the extension).
- **fileExtension** (`string`): The file extension (e.g., `.xlsx`, `.csv`, `.pdf`).
- **data** (`Blob`): The data to be downloaded.

This function creates a temporary anchor (`<a>`) element, sets the `download` attribute with the provided `baseFilename` and `fileExtension`, and triggers a download of the file using the data provided.

#### Example:

If you're downloading leave request data as an Excel file, the function will use the filename `'Download'`, append the `.xlsx` extension, and download the file using the Blob data.

```js
DownloadFile('Download', '.xlsx', response.data);
```

## Contributing

We welcome contributions to improve this library! If you'd like to contribute, please:

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature-branch`).
3. Commit your changes (`git commit -am 'Add new feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

This library is maintained by **Sivasaran S**.
```

### Key Sections in `README.md`:
1. **Installation**: Instructions for installing the library with `npm` or `yarn`.
2. **Usage**: Basic usage showing how to import and use the `DownloadFile` utility function.
3. **Example**: A full example using `axios` to download leave requests as different file formats (Excel, CSV, PDF).
4. **API Documentation**: A brief explanation of how the `DownloadFile` function works.
5. **Contributing**: Instructions on how to contribute to the project.
6. **License**: MIT License information.
7. **Author**: Maintainer's details (you).

This `README.md` provides clear usage instructions for developers integrating the `vamtec-react` library into their React projects. Let me know if you need any more details or adjustments!