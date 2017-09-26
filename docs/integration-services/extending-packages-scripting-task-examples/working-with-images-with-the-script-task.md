---
title: Trabalhando com imagens com a tarefa Script | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- graphics [Integration Services]
- Script task [Integration Services], images
- Drawing namespace
- images [Integration Services]
- SSIS Script task, images
- Script task [Integration Services], examples
- thumbnails [Integration Services]
- System.Drawing namespace
- JPEG format [Integration Services]
- .jpeg files
ms.assetid: 74aeb7ab-51b2-4b9f-84ee-0b46a7908ab9
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4a28fe7c6024d8cf5669199e5f33e3532013e4d3
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="working-with-images-with-the-script-task"></a>Trabalhando com imagens com a tarefa Script
  Um banco de dados de produtos ou usuários costuma incluir imagens além de texto e dados numéricos. O **System. Drawing** namespace no Microsoft .NET Framework fornece classes para manipulação de imagens.  
  
 [Exemplo 1: Converta imagens no formato JPEG](#example1)  
  
 [Exemplo 2: Criar e salvar imagens em miniatura](#example2)  
  
> [!NOTE]  
>  Se desejar criar uma tarefa mais fácil de ser reutilizada em vários pacotes, procure utilizar o código desse exemplo de tarefa Script como o ponto inicial de uma tarefa personalizada. Para obter mais informações, consulte [Desenvolvendo uma tarefa personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
##  <a name="example1"></a>Descrição do exemplo 1: Converta imagens no formato JPEG  
 O exemplo a seguir abre um arquivo de imagem especificado por uma variável e salva-o como um arquivo JPEG compactado usando um codificador. O código para recuperar informações de codificador é encapsulado em uma função particular.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>Para configurar esse exemplo de tarefa Script para uso com um único arquivo de imagem  
  
1.  Crie uma variável de cadeia de caracteres nomeada `CurrentImageFile` e defina seu valor com o caminho e nome de arquivo de um arquivo de imagem existente.  
  
2.  No **Script** página do **Editor da tarefa Script**, adicionar o `CurrentImageFile` variável para o **ReadOnlyVariables** propriedade.  
  
3.  No projeto de script, defina uma referência o **System. Drawing** namespace.  
  
4.  No seu código, use **Imports** instruções para importar o **System. Drawing** e **System.IO** namespaces.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>Para configurar esse exemplo de tarefa Script para uso com vários arquivos de imagem  
  
1.  Coloque a tarefa Script dentro de um contêiner do Loop Foreach.  
  
2.  No **coleção** página do **Editor de Loop Foreach**, selecione o **enumerador de arquivo Foreach** como o enumerador e especifique a máscara de arquivo e caminho da fonte de arquivos, como como "*.bmp".  
  
3.  Sobre o **mapeamentos de variáveis** página, mapeie o `CurrentImageFile` variável para o índice 0. Essa variável passa o nome de arquivo atual para a tarefa Script em cada iteração do enumerador.  
  
    > [!NOTE]  
    >  Essas etapas são adicionais às etapas listadas no procedimento para uso com um único arquivo de imagem.  
  
### <a name="example-1-code"></a>Código de exemplo 1  
  
```vb  
Public Sub Main()  
  
    'Create and initialize variables.  
    Dim currentFile As String  
    Dim newFile As String  
    Dim bmp As Bitmap  
    Dim eps As New Imaging.EncoderParameters(1)  
    Dim ici As Imaging.ImageCodecInfo  
    Dim supportedExtensions() As String = _  
        {".BMP", ".GIF", ".JPG", ".JPEG", ".EXIF", ".PNG", _  
        ".TIFF", ".TIF", ".ICO", ".ICON"}  
  
    Try  
        'Store the variable in a string for local manipulation.  
        currentFile = Dts.Variables("CurrentImageFile").Value.ToString  
        'Check the extension of the file against a list of  
        'files that the Bitmap class supports.  
        If Array.IndexOf(supportedExtensions, _  
            Path.GetExtension(currentFile).ToUpper) > -1 Then  
  
            'Load the file.  
            bmp = New Bitmap(currentFile)  
  
            'Calculate the new name for the compressed image.  
            'Note: This will overwrite existing JPEGs.  
            newFile = Path.Combine( _  
                Path.GetDirectoryName(currentFile), _  
                String.Concat(Path.GetFileNameWithoutExtension(currentFile), _  
                ".jpg"))  
  
            'Specify the compression ratio (0=worst quality, 100=best quality).  
            eps.Param(0) = New Imaging.EncoderParameter( _  
                Imaging.Encoder.Quality, 75)  
  
            'Retrieve the ImageCodecInfo associated with the jpeg format.  
            ici = GetEncoderInfo("image/jpeg")  
  
            'Save the file, compressing it into the jpeg encoding.  
            bmp.Save(newFile, ici, eps)  
        Else  
            'The file is not supported by the Bitmap class.  
            Dts.Events.FireWarning(0, "Image Resampling Sample", _  
                "File " & currentFile & " is not a supported format.", _  
                "", 0)  
         End If  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Image Resampling Sample", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Function GetEncoderInfo(ByVal mimeType As String) As Imaging.ImageCodecInfo  
  
    'The available image codecs are returned as an array,  
    'which requires code to iterate until the specified codec is found.  
  
    Dim count As Integer  
    Dim encoders() As Imaging.ImageCodecInfo  
  
    encoders = Imaging.ImageCodecInfo.GetImageEncoders()  
  
    For count = 0 To encoders.Length  
        If encoders(count).MimeType = mimeType Then  
            Return encoders(count)  
        End If  
    Next  
  
    'This point is only reached if a codec is not found.  
    Err.Raise(513, "Image Resampling Sample", String.Format( _  
        "The {0} codec is not available. Unable to compress file.", _  
            mimeType))  
    Return Nothing  
  
End Function  
  
```  
  
##  <a name="example2"></a>Descrição do exemplo 2: Criar e salvar imagens em miniatura  
 O exemplo a seguir abre um arquivo de imagem especificado por uma variável, cria uma miniatura da imagem, mantendo uma taxa de proporção constante e salva a miniatura com um nome de arquivo modificado. O código que calcula a altura e largura da miniatura, mantendo uma taxa de proporção constante, é encapsulado em uma sub-rotina particular.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>Para configurar esse exemplo de tarefa Script para uso com um único arquivo de imagem  
  
1.  Crie uma variável de cadeia de caracteres nomeada `CurrentImageFile` e defina seu valor com o caminho e nome de arquivo de um arquivo de imagem existente.  
  
2.  Também crie a variável de inteiro `MaxThumbSize` e atribua um valor em pixels, como 100.  
  
3.  No **Script** página do **Editor da tarefa Script**, adicione as duas variáveis para o **ReadOnlyVariables** propriedade.  
  
4.  No projeto de script, defina uma referência o **System. Drawing** namespace.  
  
5.  No seu código, use **Imports** instruções para importar o **System. Drawing** e **System.IO** namespaces.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>Para configurar esse exemplo de tarefa Script para uso com vários arquivos de imagem  
  
1.  Coloque a tarefa Script dentro de um contêiner do Loop Foreach.  
  
2.  No **coleção** página do **Editor de Loop Foreach**, selecione o **enumerador de arquivo Foreach** como o **enumerador**e especificar o máscara de arquivo e caminho dos arquivos de origem, como "jpg".  
  
3.  Sobre o **mapeamentos de variáveis** página, mapeie o `CurrentImageFile` variável para o índice 0. Essa variável passa o nome de arquivo atual para a tarefa Script em cada iteração do enumerador.  
  
    > [!NOTE]  
    >  Essas etapas são adicionais às etapas listadas no procedimento para uso com um único arquivo de imagem.  
  
### <a name="example-2-code"></a>Código de exemplo 2  
  
```vb  
Public Sub Main()  
  
    Dim currentImageFile As String  
    Dim currentImage As Image  
    Dim maxThumbSize As Integer  
    Dim thumbnailImage As Image  
    Dim thumbnailFile As String  
    Dim thumbnailHeight As Integer  
    Dim thumbnailWidth As Integer  
  
    currentImageFile = Dts.Variables("CurrentImageFile").Value.ToString  
    thumbnailFile = Path.Combine( _  
        Path.GetDirectoryName(currentImageFile), _  
        String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), _  
        "_thumbnail.jpg"))  
  
    Try  
        currentImage = Image.FromFile(currentImageFile)  
  
        maxThumbSize = CType(Dts.Variables("MaxThumbSize").Value, Integer)  
        CalculateThumbnailSize( _  
            maxThumbSize, currentImage, thumbnailWidth, thumbnailHeight)  
  
        thumbnailImage = currentImage.GetThumbnailImage( _  
           thumbnailWidth, thumbnailHeight, Nothing, Nothing)  
        thumbnailImage.Save(thumbnailFile)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, "Script Task Example", _  
        ex.Message & ControlChars.CrLf & ex.StackTrace, _  
        String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Sub CalculateThumbnailSize( _  
    ByVal maxSize As Integer, ByVal sourceImage As Image, _  
    ByRef thumbWidth As Integer, ByRef thumbHeight As Integer)  
  
    If sourceImage.Width > sourceImage.Height Then  
        thumbWidth = maxSize  
        thumbHeight = CInt((maxSize / sourceImage.Width) * sourceImage.Height)  
    Else  
        thumbHeight = maxSize  
        thumbWidth = CInt((maxSize / sourceImage.Height) * sourceImage.Width)  
    End If  
  
End Sub  
```  
  
```csharp  
bool ThumbnailCallback()  
        {  
            return false;  
        }  
        public void Main()  
        {  
  
            string currentImageFile;  
            Image currentImage;  
            int maxThumbSize;  
            Image thumbnailImage;  
            string thumbnailFile;  
            int thumbnailHeight = 0;  
            int thumbnailWidth = 0;  
  
            currentImageFile = Dts.Variables["CurrentImageFile"].Value.ToString();  
            thumbnailFile = Path.Combine(Path.GetDirectoryName(currentImageFile), String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), "_thumbnail.jpg"));  
  
            try  
            {  
  
                currentImage = Image.FromFile(currentImageFile);  
  
                maxThumbSize = (int)Dts.Variables["MaxThumbSize"].Value;  
                CalculateThumbnailSize(maxThumbSize, currentImage, ref thumbnailWidth, ref thumbnailHeight);  
  
                Image.GetThumbnailImageAbort myCallback = new Image.GetThumbnailImageAbort(ThumbnailCallback);  
  
                thumbnailImage = currentImage.GetThumbnailImage(thumbnailWidth, thumbnailHeight, ThumbnailCallback, IntPtr.Zero);  
                thumbnailImage.Save(thumbnailFile);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
  
        private void CalculateThumbnailSize(int maxSize, Image sourceImage, ref int thumbWidth, ref int thumbHeight)  
        {  
  
            if (sourceImage.Width > sourceImage.Height)  
            {  
                thumbWidth = maxSize;  
                thumbHeight = (int)(sourceImage.Height * maxSize / sourceImage.Width);  
            }  
            else  
            {  
                thumbHeight = maxSize;  
                thumbWidth = (int)(sourceImage.Width * maxSize / sourceImage.Height);  
  
            }  
  
        }  
  
```  
  
  
