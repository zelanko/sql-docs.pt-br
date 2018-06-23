---
title: Alternar um banco de dados do Analysis Services entre os modos ReadOnly e ReadWrite | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ReadOnly property
- ReadWriteMode command
- operations [Analysis Services - multidimensional data]
ms.assetid: 4eff8181-08dd-4fad-b091-d400fc21a020
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 184a674d03e6c8fb6b30d10b91b2a58225894ba2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006220"
---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>Alternar um banco de dados do Analysis Services entre os modos ReadOnly e ReadWrite
  Geralmente há situações quando um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] administrador de banco de dados (dba) quer alterar o modo de leitura/gravação de um banco de dados tabular ou multidimensional. Essas situações frequentemente são conduzidas pelas necessidades comerciais, como o banco de dados entre um pool de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] servidores para uma melhor experiência de usuário.  
  
 Um modo de banco de dados pode ser alternado de várias formas. Este documento explica os cenários comuns a seguir:  
  
-   Usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Usando o AMO de maneira programática  
  
-   Por script usando XMLA  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>Para alternar o modo leitura/gravação de um banco de dados de maneira interativa usando o Management Studio  
  
1.  Localize o banco de dados a ser alternado no painel esquerdo ou direito do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  O banco de dados e selecione **propriedades**. Localize a pasta do banco de dados e anote o local. Um local de armazenamento de banco de dados vazio indica que a pasta de banco de dados está localizada na pasta de dados do servidor.  
  
    > [!IMPORTANT]  
    >  Assim que o banco de dados for desanexado, o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] já não pode lhe ajudar a obter o local do banco de dados.  
  
3.  Clique com o botão direito do mouse no banco de dados e selecione **Desanexar...**  
  
4.  Atribua uma senha ao banco de dados a ser desanexado e clique em **OK** para executar o comando Desanexar.  
  
5.  Localize o **bancos de dados** pasta no painel esquerdo ou direito de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
6.  Clique com botão direito do **bancos de dados** pasta e selecione **anexar...**  
  
7.  Na caixa de texto **pasta** , digite o local original da pasta do banco de dados. Como alternativa, use o botão Procurar (**…**) para localizar a pasta do banco de dados.  
  
8.  Selecione o modo leitura/gravação do banco de dados.  
  
9. Digite a senha que foi usada na etapa 3 e clique em **Okey** para executar o comando anexar.  
  
#### <a name="to-switch-the-readwrite-mode-to-a-database-programmatically-using-amo"></a>Para alternar o modo leitura/gravação em um banco de dados usando o AMO de maneira programática  
  
1.  Em seu aplicativo C#, adapte o seguinte código de amostra e conclua as tarefas indicadas.  
  
 `private void SwitchReadWrite(Server server, string dbName,`  
  
 `ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `string databaseLocation;`  
  
 `db = server.Databases[dbName];`  
  
 `databaseLocation = db.DbStorageLocation;`  
  
 `if (databaseLocation == null)`  
  
 `{`  
  
 `string dataDir = server.ServerProperties["DataDir"].Value;`  
  
 `String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);`  
  
 `if (possibleFolders.Length > 1)`  
  
 `{`  
  
 `List<String> sortedFolders = new List<string>(possibleFolders.Length);`  
  
 `sortedFolders.AddRange(possibleFolders);`  
  
 `sortedFolders.Sort();`  
  
 `databaseLocation = sortedFolders[sortedFolders.Count - 1];`  
  
 `}`  
  
 `else`  
  
 `{`  
  
 `databaseLocation = possibleFolders[0];`  
  
 `}`  
  
 `}`  
  
 `db.Detach();`  
  
 `server.Attach(databaseLocation, dbReadWriteMode);`  
  
 `}`  
  
 `}`  
  
1.  Em seu aplicativo C#, chame `SwitchReadWrite()` com os parâmetros necessários.  
  
2.  Compile e execute seu código para mover o banco de dados.  
  
#### <a name="to-switch-the-readwrite-mode-to-a-database-by-script-using-xmla"></a>Para alternar o modo leitura/gravação para um banco de dados por script usando XMLA  
  
1.  Localize o banco de dados a ser alternado no painel esquerdo ou direito do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  O banco de dados e selecione **propriedades**. Localize a pasta do banco de dados e anote o local. Um local de armazenamento de banco de dados vazio indica que a pasta de banco de dados está localizada na pasta de dados do servidor.  
  
    > [!IMPORTANT]  
    >  Assim que o banco de dados for desanexado, o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] já não pode lhe ajudar a obter o local do banco de dados.  
  
3.  Abra uma nova guia XMLA em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
4.  Copie o modelo de script a seguir para XMLA:  
  
 `<Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  Substitua `%dbName%` pelo nome do banco de dados e `%password%` pela senha. Os caracteres % fazem parte do modelo e devem ser removidos.  
  
2.  Execute o comando XMLA.  
  
3.  Copiar o modelo de script a seguir para XMLA em uma nova guia XMLA  
  
 `<Attach xmlns="http://schemas.microsoft.com/analysisservices/2003` `/engine` `">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  Substitua `%dbFolder%` pelo caminho UNC completo da pasta do banco de dados, `%ReadOnlyMode%` pelo valor correspondente `ReadOnly` ou `ReadWrite` e `%password%` pela senha. Os caracteres % fazem parte do modelo e devem ser removidos.  
  
2.  Execute o comando XMLA.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Anexar e desanexar bancos de dados do Analysis Services](attach-and-detach-analysis-services-databases.md)   
 [Local de armazenamento do banco de dados](database-storage-location.md)   
 [Banco de dados ReadWriteModes](database-readwritemodes.md)   
 [Elemento Attach](../xmla/xml-elements-commands/attach-element.md)   
 [Elemento Detach](../xmla/xml-elements-commands/detach-element.md)   
 [Elemento ReadWriteMode](../xmla/xml-elements-properties/readwritemode-element.md)   
 [Elemento DbStorageLocation](../xmla/xml-elements-properties/dbstoragelocation-element.md)  
  
  