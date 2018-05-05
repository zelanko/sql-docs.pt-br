---
title: Mover um Analysis Services do banco de dados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7f74a707efefe7b94122462a8a229c1585766207
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="move-an-analysis-services-database"></a>Mover um banco de dados do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Frequentemente, há situações em que um dba (administrador de banco de dados) [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quer mover um modelo de banco de dados multidimensional ou de tabela para um local diferente. Essas situações frequentemente são conduzidas pelas necessidades comerciais, como a movimentação do banco de dados para um disco diferente em busca de um melhor desempenho, a obtenção de espaço para o crescimento do banco de dados ou para a atualização de um produto.  
  
 Um banco de dados pode ser movido de muitas formas. Este documento explica os cenários comuns a seguir:  
  
-   Usando o SSMS de modo interativo  
  
-   Usando o AMO de maneira programática  
  
-   Por script usando XMLA  
  
 Todos os cenários exigem que o usuário acesse a pasta do banco de dados e use um método para mover os arquivos para o destino final desejado.  
  
> [!NOTE]  
>  Desanexar um banco de dados sem atribuir uma senha a ele deixa o banco de dados em um estado não seguro. Recomendamos atribuir uma senha ao banco de dados para proteger informações confidenciais. Além disso, a segurança de acesso correspondente deve ser aplicada à pasta do banco de dados, subpastas e arquivos para impedir o acesso não autorizado a ele.  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="moving-a-database-interactively-using-ssms"></a>Movendo um banco de dados de maneira interativa usando SSMS  
  
1.  Localize o banco de dados a ser movido no painel esquerdo ou direito do SSMS.  
  
2.  Clique com o botão direito do mouse no banco de dados e selecione **Desanexar...**  
  
3.  Atribua uma senha ao banco de dados a ser desanexado e clique em **OK** para executar o comando detach.  
  
4.  Use qualquer mecanismo de sistema operacional ou método padrão para mover arquivos para mover a pasta do banco de dados para o novo local.  
  
5.  Localize a pasta **Bancos de Dados** no painel esquerdo ou direito do SSMS.  
  
6.  Clique com o botão direito do mouse na pasta **Bancos de Dados** e selecione **Anexar...**  
  
7.  Na caixa de texto **pasta** , digite o novo local da pasta do banco de dados. Como alternativa, use o botão Procurar (**…**) para localizar a pasta do banco de dados.  
  
8.  Selecione o modo **ReadWrite** do banco de dados.  
  
9. Digite a senha usada na etapa 3 e clique em **OK** para executar o comando Anexar.  
  
#### <a name="moving-a-database-programmatically-using-amo"></a>Movendo um banco de dados que usa AMO programaticamente  
  
1.  Em seu aplicativo C#, adapte o seguinte código de amostra e conclua as tarefas indicadas.  
  
 `private void MoveDb(Server server, string dbName,`  
  
 `string dbInitialLocation, string dbFinalLocation,`  
  
 `string dbPassword, ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `//Verify dbInitialLocation exists before continuing`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `//Save current cursor and change cursor to Cursors.WaitCursor`  
  
 `db = server.Databases[dbName];`  
  
 `db.Detach(dbPassword);`  
  
 `//Add your own code to copy the database files to the destination where you intend to attach the database`  
  
 `//Verify dbFinalLocation exists before continuing`  
  
 `server.Attach(dbFinalLocation, dbReadWriteMode, dbPassword);`  
  
 `//Restore cursor to its original`  
  
 `}`  
  
 `}`  
  
1.  Em seu aplicativo C#, chame `MoveDb()` com os parâmetros necessários.  
  
2.  Compile e execute seu código para mover o banco de dados.  
  
#### <a name="moving-a-database-by-script-using-xmla"></a>Movendo um banco de dados por script usando XMLA  
  
1.  Abra uma nova guia XMLA no SSMS.  
  
2.  Copie o modelo de script a seguir para XMLA  
  
 `<Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  Substitua `%dbName%` pelo nome do banco de dados e `%password%` pela senha. Os caracteres % fazem parte do modelo e devem ser removidos.  
  
2.  Execute o comando XMLA.  
  
3.  Use qualquer mecanismo de sistema operacional ou método padrão para mover arquivos para mover a pasta do banco de dados para o novo local.  
  
4.  Copiar o modelo de script a seguir para XMLA em uma nova guia XMLA  
  
 `<Attach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  Substitua `%dbFolder%` pelo caminho UNC completo da pasta do banco de dados, `%ReadOnlyMode%` pelo valor correspondente **ReadOnly** ou **ReadWrite**e `%password%` pela senha. Os caracteres % fazem parte do modelo e devem ser removidos.  
  
2.  Execute o comando XMLA.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.Core.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Anexar e desanexar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Local de armazenamento do banco de dados](../../analysis-services/multidimensional-models/database-storage-location.md)   
 [Banco de dados ReadWriteModes](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Elemento Attach](../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Elemento Detach](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Elemento ReadWriteMode](../../analysis-services/xmla/xml-elements-properties/readwritemode-element.md)   
 [Elemento DbStorageLocation](../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)  
  
  
