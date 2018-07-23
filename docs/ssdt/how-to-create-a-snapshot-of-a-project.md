---
title: Como criar um instantâneo de um projeto | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.SqlProjectImportSnapshotSummaryDialog.dialog
- sql.data.tools.SqlProjectImportSnapshotDialog.dialog
ms.assetid: bed670a3-13bd-4d88-91a1-58d5b9524a97
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 34430ec8b9da41806e86a0b7fa6de99057765aca
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39088298"
---
# <a name="how-to-create-a-snapshot-of-a-project"></a>Como: Criar um instantâneo de um projeto
Um arquivo de **Aplicativo da camada de dados** fornece uma representação somente leitura do esquema de banco de dados no momento em que ele é criado. Ele está sendo tratado basicamente como um esquema de banco de dados do qual você pode importar os objetos de esquema de volta para um projeto. Você também pode compará-lo com o esquema de um banco de dados ou um projeto e atualizar o banco de dados ou o projeto para refletir o esquema definido no instantâneo.  
  
No caso de um erro do usuário em um projeto de banco de dados de origem, você poderá reverter projeto de origem ao estado em que estava quando o instantâneo foi criado. Você também pode estabelecer instantâneos em várias fases de seu desenvolvimento para a finalidade de linha de base.  
  
> [!WARNING]  
> Os procedimentos a seguir utilizam entidades criadas em procedimentos anteriores nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-create-a-snapshot"></a>Para criar um instantâneo  
  
1.  Clique com o botão direito do mouse no projeto **TradeDev** no **Gerenciador de Soluções** e selecione **Aplicativo da Camada de Dados (\*.dacpac)…**.  
  
2.  O SSDT tentará compilar o projeto primeiro. Se não houver nenhum erro de compilação, uma pasta **Instantâneo** será criada no **Gerenciador de Soluções**. Dentro dessa pasta, o SSDT cria um arquivo .dacpac com o mesmo formato de nome de "<Project Name>_AAAAMMDD_HH-MM-SS.dacpac".  
  
3.  Clique com o botão direito do mouse no arquivo .dacpac e selecione **Renomear**. Altere o nome de arquivo padrão para "TradeDev1.dacpac."  
  
4.  Clique com o botão direito do mouse na função **GetProductsBySupplier** no **Gerenciador de Soluções** e selecione **Excluir** para removê-la do projeto.  
  
5.  Siga as etapas anteriores para criar um novo instantâneo chamado **TradeDev2.dacpac**.  
  
### <a name="to-import-a-snapshot"></a>Para importar um instantâneo  
  
1.  Clique com o botão direito do mouse no projeto **TradeDev** no **Gerenciador de Soluções** e selecione **Importar** e **Aplicativo da Camada de Dados (\*.dacpac)…** nos menus contextuais.  
  
2.  Na caixa de diálogo **Importar Aplicativo da Camada de Dados**, clique em **Procurar** para selecionar **TradeDev1.dacpac** para ser usado como a origem da importação.  
  
    Observe que a seção **Projeto de destino** foi desabilitada, já que o projeto atual é o destino padrão. Clique em **Iniciar** para iniciar a importação.  
  
3.  Clique em **Concluir** na página **Resumo**. No **Gerenciador de Soluções**, observe que a tabela excluída foi restaurada para o projeto.  
  
    > [!WARNING]  
    > O instantâneo de importação importará todas as entidades de banco de dados no esquema de instantâneo para o projeto. Isto pode criar entidades duplicadas como resultado. Por exemplo, cada uma das tabelas e exibições agora contém uma cópia adicional de si mesma chamada <ObjectName_1>. Clique com o botão direito do mouse em cada um desses objetos duplicados no **Gerenciador de Soluções** e selecione **Excluir** para removê-lo do projeto.  
  
### <a name="to-compare-snapshots"></a>Para comparar instantâneos  
  
1.  Clique com o botão direito do mouse em **TradeDev1.dacpac** no Gerenciador de Soluções e selecione **Comparação de Esquemas**. A janela **Comparação de Esquemas** é aberta.  
  
2.  Use as opções do **Arquivo de Aplicativo da Camada de Dados** para definir os esquemas de origem e destino. Verifique se o **Esquema de Origem** está definido como **TradeDev1.dacpac** no **Arquivo de Aplicativo da Camada de Dados** e se o **Esquema de Destino** está definido como **TradeDev2.dacpac**.  
  
3.  Clique em **OK** para iniciar a comparação. Observe que a função excluída está sendo realçada como uma diferença entre o instantâneo antigo e o novo.  
  
    Você pode localizar facilmente o delta de instantâneos diferentes usando a Comparação de Esquemas. Neste caso, você pode descobrir como seu projeto evolui durante o processo de desenvolvimento.  
  
## <a name="see-also"></a>Consulte Também  
[Como usar comparação de esquema para comparar definições de banco de dados diferentes](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
