---
title: "Gerenciador de Conexão do Hadoop | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.hadoopconn.f1
ms.assetid: 8bb15b97-9827-46bc-aca6-068534ab18c4
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 79b0782d0d01733f10310f1eaac611fc688dbf21
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="hadoop-connection-manager"></a>Gerenciador de conexões do Hadoop
  O gerenciador de conexões do Hadoop permite que um pacote do SSIS se conecte a um cluster Hadoop usando os valores especificados para as propriedades.  
  
## <a name="configure-the-hadoop-connection-manager"></a>Configurar o Gerenciador de Conexões do Hadoop  
  
1.  Na caixa de diálogo **Adicionar Gerenciador de Conexões do SSIS** , escolha **Hadoop**e clique em **Adicionar**. A caixa de diálogo **Gerenciador de conexões do Hadoop** se abre.  
  
2.  Escolha a guia **WebHCat** ou **WebHDFS** no painel esquerdo para configurar informações relacionadas ao cluster Hadoop.  
  
3.  Se você habilitar a opção **WebHCat** para invocar um trabalho de Hive ou Pig no Hadoop, faça o seguinte.  
  
    1.  Para o **Hóspede WebHCat**, insira o servidor que hospeda o serviço WebHCat.  
  
    2.  Para a **Porta WebHCat**, insira a porta do serviço WebHCat, que é 50111 por padrão.  
  
    3.  Escolha o método de **Autenticação** para acessar o serviço WebHCat. Os valores disponíveis são **Básico** e **Kerberos**.  
  
         ![Editor de Gerenciador de conexão do Hadoop com a autenticação básica](../../integration-services/connection-manager/media/hadoop-cm-basic.png "Hadoop editor do Gerenciador de conexão com a autenticação básica")  
  
         ![Editor de Gerenciador de conexão do Hadoop com a autenticação Kerberos](../../integration-services/connection-manager/media/hadoop-cm-kerberos.png "Hadoop editor do Gerenciador de conexão com a autenticação Kerberos")  
  
    4.  Para o **Usuário WebHCat**, insira o **Usuário** autorizado a acessar o WebHCat.  
  
    5.  Se você escolher a autenticação **Kerberos** , insira a **Senha** e o **Domínio**do usuário.  
  
4.  Se você habilitar a opção **WebHDFS** para copiar dados de ou para o HDFS, faça o seguinte.  
  
    1.  Para o **Hóspede WebHDFS**, insira o servidor que hospeda o serviço WebHDFS.  
  
    2.  Para a **Porta WebHDFS**, insira a porta do serviço WebHDFS, que é 50070 por padrão.  
  
    3.  Selecione o método de **Autenticação** para acessar o serviço WebHDFS. Os valores disponíveis são **Básico** e **Kerberos**.  
  
    4.  Para o **Usuário WebHDFS**, insira o usuário autorizado a acessar o HDFS.  
  
    5.  Se você escolher a autenticação **Kerberos** , insira a **Senha** e o **Domínio**do usuário.  
  
5.  Clique em **Testar Conexão** para testar a conexão. (Apenas a conexão que você habilitou é testada.)  
  
6.  Clique em **OK** para fechar a caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa do Hive do Hadoop](../../integration-services/control-flow/hadoop-hive-task.md)   
 [Tarefa de Pig do Hadoop](../../integration-services/control-flow/hadoop-pig-task.md)   
 [Tarefas do sistema de arquivos Hadoop](../../integration-services/control-flow/hadoop-file-system-task.md)  
  
  
