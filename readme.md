This **code** might help
* Use this
* using System.IO;
* using System.IO.Compression;
*
~~~~
public void ComprimirArchivo(string rutaFinal, string nombreArchivoXML, string nombreArchivoZip)
{
	//string rutaArchivo = @"F:\Archivos\FACTURACION_ELECTRONICA\xmlPrueba\firmados\20100762936-01-F001-0000006.xml";
	//string outPutFileName = @"F:\Archivos\FACTURACION_ELECTRONICA\xmlPrueba\firmados\20100762936-01-F001-0000006.zip";
	string rutaArchivo = rutaFinal + nombreArchivoXML;
	string outPutFileName = rutaFinal + nombreArchivoZip;
	using (ZipArchive zip = ZipFile.Open(outPutFileName, ZipArchiveMode.Create))
	{
		//zip.CreateEntryFromFile(rutaArchivo, "20100762936-01-F001-0000006.xml");
		zip.CreateEntryFromFile(rutaArchivo, nombreArchivoXML);
	}
}

public string DecomprimirArchivo(string rutaFinal, string nombreArchivoZip)
{
	//string rutaArchivo = @"F:\Archivos\FACTURACION_ELECTRONICA\xmlPrueba\firmados\";
	//string outPutFileName = @"F:\Archivos\FACTURACION_ELECTRONICA\xmlPrueba\firmados\R-20100762936-01-F001-0000006.zip";
	string rutaArchivo = rutaFinal;
	string outPutFileName = nombreArchivoZip;
	string cadena = "";
	using (ZipArchive zip = ZipFile.OpenRead(outPutFileName))
	{
		foreach (ZipArchiveEntry entry in zip.Entries)
		{
			if (entry.FullName.EndsWith(".xml", StringComparison.OrdinalIgnoreCase))
			{
				entry.ExtractToFile(Path.Combine(rutaArchivo, entry.FullName));
				cadena = entry.FullName;
			}
		}
	}
	return cadena;
}
~~~~