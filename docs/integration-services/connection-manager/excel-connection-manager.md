---
title: Gerenciador de conexões do Excel | Microsoft Docs
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fdac3f09fa3b92d7babd9c43f5a71adc4191ac7e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923712"
---
# <a name="excel-connection-manager"></a>Gerenciador de conexões do Excel

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Um gerenciador de conexões do Excel permite a conexão de um pacote a um arquivo de pasta de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel. A origem e o destino do Excel que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui usam o gerenciador de conexões do Excel.  
 
> [!IMPORTANT]
> Para obter informações detalhadas sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md).

 Quando você adiciona um gerenciador de conexões do Excel a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que é resolvido como uma conexão do Excel em tempo de execução, define as propriedades do gerenciador de conexões e o adiciona à coleção **Coleções** no pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **EXCEL**.  
  
## <a name="configure-the-excel-connection-manager"></a>Configurar o Gerenciador de conexões do Excel  
 Você pode configurar o gerenciador de conexões do Excel dos seguintes modos:  
  
-   Especificando o caminho do arquivo de pasta de trabalho Excel.  
  
-   Especificando a versão do Excel que foi usada para criar o arquivo.  
  
-   Indique se a primeira linha nas planilhas ou intervalos selecionados contém nomes de coluna.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões do Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="excel-connection-manager-editor"></a>Editor de Gerenciador de Conexões Excel
  Use a caixa de diálogo **Editor de Gerenciador de Conexões Excel** para adicionar uma conexão a um arquivo da pasta de trabalho novo ou existente do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] .  
  
### <a name="options"></a>Opções  
 **Caminho de arquivo do Excel**  
 Digite o caminho e o nome do arquivo de um arquivo de pasta de trabalho novo ou existente do Excel.  
   
 **Procurar**  
 Use a caixa de diálogo **Abrir** para navegar até a pasta na qual o arquivo Excel existe ou na qual você deseja criar o novo arquivo.  
  
 **Versão do Excel**  
 Especifique a versão do Microsoft Excel que foi usada para criar o arquivo.  
  
 **Primeira linha com nomes de coluna**  
 Especifique se a primeira linha de dados na planilha selecionada contém os nomes de coluna. O valor padrão desta opção é **Verdadeiro**.  

## <a name="solution-to-import-data-with-mixed-data-types-from-excel"></a>Solução para importar dados com tipos de dados mistos do Excel

Se você usar dados que contenham tipos de dados mistos, por padrão, o driver do Excel lerá as oito primeiras linhas (configuradas pela chave de registro **TypeGuessRows**). Com base nas oito primeiras linhas de dados, o driver do Excel tenta adivinhar o tipo de dados de cada coluna. Por exemplo, se a fonte de dados do Excel tiver números e texto em uma coluna, se as oito primeiras linhas contiverem números, o driver poderá determinar com base nessas oito primeiras linhas que os dados na coluna são do tipo inteiro. Nesse caso, o SSIS ignora valores de texto e os importa como NULO no destino.

Para resolver esse problema, você pode usar uma das seguintes soluções:

* Altere o tipo de coluna do Excel para **Texto** no arquivo do Excel.
* Adicione a propriedade estendida IMEX à cadeia de conexão para substituir o comportamento padrão do driver. Ao adicionar a propriedade estendida ";IMEX=1" ao final da cadeia de conexão, o Excel trata todos os dados como texto. Consulte o seguinte exemplo:
    
  ```ACE OLEDB connection string:
  Provider=Microsoft.ACE.OLEDB.12.0;Data Source=C:\ExcelFileName.xlsx;Extended Properties="EXCEL 12.0 XML;HDR=YES;IMEX=1";
  ```

   Para que essa solução funcione de forma confiável, talvez seja necessário modificar também as configurações do registro. O arquivo main.cmd é o seguinte:
  
   ```cmd
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\12.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\12.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\15.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   ```

* Salve o arquivo no formato CSV e altere o pacote SSIS para ser compatível com uma importação de CSV.

## <a name="related-tasks"></a>Related Tasks  
[Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)  
[Origem do Excel](../data-flow/excel-source.md)  
[Destino do Excel](../data-flow/excel-destination.md)
