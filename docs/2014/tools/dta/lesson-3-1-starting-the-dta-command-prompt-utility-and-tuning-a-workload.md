---
title: Iniciando o utilitário de prompt de comando dta e ajustando uma carga de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: f34a5acf-1f3b-4484-a770-6470cb925ab0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf882bc731c8e435de808092e990b35ad23ce57e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66110154"
---
# <a name="starting-the-dta-command-prompt-utility-and-tuning-a-workload"></a>Iniciando o utilitário de prompt de comando dta e ajustando uma carga de trabalho
  Essa tarefa descreve a inicialização do utilitário **dta** , a exibição da Ajuda e o uso do utilitário para ajustar uma carga de trabalho no prompt de comando. Ela usa a carga de trabalho MyScript.sql, criada para a prática [Ajustando uma carga de trabalho](lesson-1-1-tuning-a-workload.md)da GUI (interface gráfica do usuário) do Orientador de Otimização do Mecanismo de Banco de Dados.  
  
 O tutorial usa o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Por motivos de segurança, os bancos de dados de exemplo não são instalados por padrão. Para instalar os bancos de dados de exemplo, consulte [Instalando amostras e bancos de dados de exemplo do SQL Server](http://sqlserversamples.codeplex.com).  
  
 As tarefas a seguir descrevem a abertura de um prompt de comando, a inicialização do utilitário de prompt de comando **dta** , a exibição da Ajuda sobre a sintaxe e o ajuste de uma carga de trabalho simples, MyScript.sql, que você criou em [Ajustando uma carga de trabalho](lesson-1-1-tuning-a-workload.md).  
  
### <a name="to-start-the-dta-command-prompt-utility-and-view-help"></a>Para iniciar o utilitário de prompt de comando dta e exibir a Ajuda  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para **Acessórios**e clique em **Prompt de Comando**.  
  
2.  No prompt de comando, digite o seguinte e pressione ENTER:  
  
    ```  
    dta -? | more  
    ```  
  
     A parte `| more` desse comando é opcional. Porém, seu uso permite que você pesquise na sintaxe de ajuda do utilitário. Pressione ENTER para avançar o texto de ajuda pela linha ou pressione a SPACEBAR para avançar por página.  
  
### <a name="to-tune-a-simple-workload-by-using-the-dta-command-prompt-utility"></a>Para ajustar uma carga de trabalho simples usando o utilitário de prompt de comando dta  
  
1.  No prompt de comando, navegue até o diretório em que você armazenou o arquivo MyScript.sql.  
  
2.  No prompt de comando, digite o seguinte e pressione ENTER para executar o comando e iniciar a sessão de ajuste (observe que o utilitário faz diferenciação de maiúsculas e minúsculas na análise de comandos):  
  
    ```  
    dta -S YourServerName\YourSQLServerInstanceName -E -D AdventureWorks2012 -if MyScript.sql -s MySession2 -of MySession2OutputScript.sql -ox MySession2Output.xml -fa IDX_IV -fp NONE -fk NONE  
    ```  
  
     onde `-S` especifica o nome de seu servidor e a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] é instalado. A configuração `-E` especifica que você quer usar uma conexão confiável com a instância, o que é apropriado se você estiver se conectando com uma conta de domínio Windows. A configuração `-D` especifica o banco de dados que você quer ajustar, `-if` especifica o arquivo de carga de trabalho, `-s` especifica o nome de sessão, `-of` especifica o arquivo para o qual você deseja que a ferramenta escreva o script de recomendações [!INCLUDE[tsql](../../includes/tsql-md.md)] e `-ox` especifica o arquivo para o qual você deseja que a ferramenta escreva as recomendações no formato XML. As três últimas opções especificam opções de ajuste como segue: `-fa IDX_IV` especifica que o Orientador de Otimização do Mecanismo de Banco de Dados só deve considerar adicionar índices (clusterizado e não clusterizado) e exibições indexadas; `-fp NONE` especifica que nenhuma estratégia de partição deve ser considerada durante a análise; e `-fk NONE` especifica que nenhuma estrutura de design física existente no banco de dados deve ser mantida quando o Orientador de Otimização do Mecanismo de Banco de Dados faz suas recomendações.  
  
3.  Depois que o Orientador de Otimização do Mecanismo de Banco de Dados termina de ajustar a carga de trabalho, exibe uma mensagem que indica que a sessão de ajuste foi concluída com êxito. Você pode exibir os resultados do ajuste, usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para abrir os arquivos MySession2OutputScript.sql e MySession2Output.xml. Como alternativa, você também pode abrir a sessão de ajuste MySession2 na GUI do Orientador de Otimização do Mecanismo de Banco de Dados e exibir suas recomendações e relatórios da mesma forma que fez em [Exibindo recomendações de ajuste](lesson-1-2-viewing-tuning-recommendations.md) e [Exibindo relatórios de ajuste](lesson-1-3-viewing-tuning-reports.md).  
  
## <a name="summary"></a>Resumo  
 Você concluiu o ajuste de uma carga de trabalho simples no prompt de comando usando o utilitário **dta** . Essa ferramenta fornece muitas outras opções de ajuste. Veja a Ajuda da ferramenta (**dta -?**) e o tópico de referência [Utilitário dta](dta-utility.md) para obter mais informações.  
  
## <a name="after-you-finish-this-tutorial"></a>Depois de você concluir este tutorial  
 Depois de você terminar as lições deste tutorial, recorra aos tópicos a seguir para obter mais informações sobre o Orientador de Otimização do Mecanismo de Banco de Dados:  
  
-   [Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md) para obter descrições sobre como executar tarefas com essa ferramenta.  
  
-   [dta Utility](dta-utility.md) para obter material de referência sobre o utilitário de prompt de comando e o arquivo XML opcional que você pode usar para controlar a operação do utilitário.  
  
 Para retornar ao início do tutorial, consulte [Tutorial: Orientador de Otimização do Mecanismo de Banco de Dados](tutorial-database-engine-tuning-advisor.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tutoriais do Mecanismo de Banco de Dados](../../relational-databases/database-engine-tutorials.md)  
  
  
