---
title: Alternar um banco de dados do Analysis Services entre os modos ReadOnly e ReadWrite | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e1ae8fc032a1f728372e9b4e764281ea8df8ddaa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63020060"
---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>Alternar um banco de dados do Analysis Services entre os modos ReadOnly e ReadWrite
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Os administradores de banco de dados do podem alterar o modo de leitura/gravação de um banco de dados Tabular ou Multidimensional como parte do esforço maior que distribui uma carga de trabalho de consulta entre vários servidores somente consulta.  
  
 Um modo de banco de dados pode ser alternado de várias formas. Este documento explica os cenários comuns a seguir:  
  
-   Usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Usando o AMO de maneira programática  
  
-   Script usando XMLA ou TMSL  
  
## <a name="switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>Alterne o modo leitura/gravação de um banco de dados de maneira interativa usando o Management Studio  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados e selecione **Propriedades**.  
  
     Anote o local. Um local de armazenamento de banco de dados vazio indica que a pasta de banco de dados está localizada na pasta de dados do servidor.  
  
2.  O banco de dados com o botão direito e selecione **desanexar...**  
  
3.  Atribua uma senha ao banco de dados a ser desanexado e clique em **OK** para executar o comando Desanexar.  
  
4.  No Pesquisador de objetos, clique com botão direito do **bancos de dados** pasta e selecione **anexar...**  
  
5.  Na caixa de texto **pasta** , digite o local original da pasta do banco de dados. Como alternativa, você pode usar o botão Procurar ( **...** ) para localizar a pasta do banco de dados.  
  
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
  
2.  O banco de dados com o botão direito e selecione **desanexar...**  
  
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
 [Elemento Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Elemento Detach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Elemento ReadWriteMode](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/readwritemode-element)   
 [Elemento DbStorageLocation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)  
  
  
