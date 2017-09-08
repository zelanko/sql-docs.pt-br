---
title: Alternar um banco de dados do Analysis Services entre os modos ReadOnly e ReadWrite | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ReadOnly property
- ReadWriteMode command
- operations [Analysis Services - multidimensional data]
ms.assetid: 4eff8181-08dd-4fad-b091-d400fc21a020
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 11eaa65564dcd59442bd8b111c0de009b00e8fd4
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>Alternar um banco de dados do Analysis Services entre os modos ReadOnly e ReadWrite
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Os administradores de banco de dados do podem alterar o modo de leitura/gravação de um banco de dados Tabular ou Multidimensional como parte do esforço maior que distribui uma carga de trabalho de consulta entre vários servidores somente consulta.  
  
 Um modo de banco de dados pode ser alternado de várias formas. Este documento explica os cenários comuns a seguir:  
  
-   Usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Usando o AMO de maneira programática  
  
-   Script usando XMLA ou TMSL  
  
## <a name="switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>Alterne o modo leitura/gravação de um banco de dados de maneira interativa usando o Management Studio  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados e selecione **Propriedades**.  
  
     Anote o local. Um local de armazenamento de banco de dados vazio indica que a pasta de banco de dados está localizada na pasta de dados do servidor.  
  
2.  Clique com o botão direito do mouse no banco de dados e selecione **Desanexar...**  
  
3.  Atribua uma senha ao banco de dados a ser desanexado e clique em **OK** para executar o comando Desanexar.  
  
4.  No Pesquisador de Objetos, clique com o botão direito do mouse na pasta **Bancos de Dados** e selecione **Anexar...**  
  
5.  Na caixa de texto **pasta** , digite o local original da pasta do banco de dados. Como alternativa, use o botão Procurar (**…**) para localizar a pasta do banco de dados.  
  
6.  Selecione o modo leitura/gravação do banco de dados.  
  
7.  Digite a senha e clique em **OK** para executar o comando Anexar.  
  
## <a name="switch-the-readwrite-mode-to-a-database-programmatically-using-amo"></a>Alterne o modo leitura/gravação em um banco de dados usando o AMO de maneira programática  
 Em seu aplicativo C#, chame `SwitchReadWrite()` com os parâmetros necessários. Compile e execute seu código para mover o banco de dados.  
  
```  
private void SwitchReadWrite(Server server, string dbName, ReadWriteMode dbReadWriteMode)  
{  
    if (server.Databases.ContainsName(dbName))  
    {  
        Database db;  
        string databaseLocation;  
        db = server.Databases[dbName];  
        databaseLocation = db.DbStorageLocation;  
  
              if (databaseLocation == null)  
            {  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
  
    String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);  
  
   if (possibleFolders.Length > 1)  
         {  
         List<String> sortedFolders = new List<string>(possibleFolders.Length);  
         sortedFolders.AddRange(possibleFolders);  
         sortedFolders.Sort();  
         databaseLocation = sortedFolders[sortedFolders.Count - 1];  
         }  
         else  
         {  
         databaseLocation = possibleFolders[0];  
          }  
        }  
    db.Detach();  
    server.Attach(databaseLocation, dbReadWriteMode);  
    }  
}  
  
```  
  
## <a name="switch-the-readwrite-mode-to-a-database-by-script-using-xmla"></a>Alterne o modo leitura/gravação para um banco de dados por script usando XMLA  
 As instruções a seguir se aplicam a bancos de dados Multidimensionais e Tabulares no modo de compatibilidade 1050, 1100 ou 1103.  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados e selecione **Propriedades**.  
  
     Anote o local. Um local de armazenamento de banco de dados vazio indica que a pasta de banco de dados está localizada na pasta de dados do servidor.  
  
2.  Clique com o botão direito do mouse no banco de dados e selecione **Desanexar...**  
  
3.  Abra uma nova guia XMLA em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
4.  Copie o modelo de script a seguir para XMLA:  
  
    ```  
    <Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Object>  
          <DatabaseID>%dbName%</DatabaseID>  
          <Password>%password%</Password>  
       </Object>  
    </Detach>  
    ```  
  
5.  Substitua `%dbName%` pelo nome do banco de dados e `%password%` pela senha. Os caracteres % fazem parte do modelo e devem ser removidos.  
  
6.  Execute o comando XMLA.  
  
7.  Copiar o modelo de script a seguir para XMLA em uma nova guia XMLA  
  
    ```  
    <Attach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Folder>%dbFolder%</Folder>  
       <ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>  
    </Attach>  
    ```  
  
8.  Substitua `%dbFolder%` pelo caminho UNC completo da pasta do banco de dados, `%ReadOnlyMode%` pelo valor correspondente **ReadOnly** ou **ReadWrite**e `%password%` pela senha. Os caracteres % fazem parte do modelo e devem ser removidos.  
  
9. Execute o comando XMLA.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Alta disponibilidade e escalabilidade no Analysis Services](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)   
 [Anexar e desanexar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Local de armazenamento do banco de dados](../../analysis-services/multidimensional-models/database-storage-location.md)   
 [Banco de dados ReadWriteModes](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Elemento Attach](../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Elemento Detach](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Elemento ReadWriteMode](../../analysis-services/xmla/xml-elements-properties/readwritemode-element.md)   
 [Elemento DbStorageLocation](../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)  
  
  
