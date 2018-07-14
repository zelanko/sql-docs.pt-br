---
title: Formas alternativas de obter uma conexão de dados (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: aebc5f3d-97d5-4d54-b525-753fed073a9a
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 6b0b08a1435a007c38511d4e93db1c2783dfa956
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37296326"
---
# <a name="alternative-ways-to-get-a-data-connection-report-builder"></a>Formas alternativas de obter uma conexão de dados (Construtor de Relatórios)
  Uma conexão de dados contém as informações para estabelecer conexões com uma fonte de dados externa, como um banco de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Geralmente, você obtém as informações sobre a conexão e o tipo de credenciais a ser usado do proprietário da fonte de dados.  
  
 Para especificar uma conexão de dados, é possível usar uma fonte de dados compartilhada do servidor de relatório ou criar uma fonte de dados inserida que será usada somente em um relatório específico.  
  
 Na maioria dos tutoriais, você usa fontes de dados inseridas, mas se tiver acesso a fontes de dados compartilhadas, você poderá usá-las.  
  
## <a name="getting-a-data-connection-from-a-shared-data-source"></a>Obtendo uma conexão de dados de uma fonte de dados compartilhada  
 Se o servidor de relatório tiver fontes de dados compartilhadas disponíveis que você possa usar, use-as em vez de uma fonte de dados inserida. Os procedimentos a seguir explicam como localizar as fontes de dados compartilhadas e como fornecer todas as credenciais necessárias para usá-las.  
  
 Para usar uma fonte de dados compartilhada, é necessário navegar até um servidor de relatório e selecioná-la. Geralmente, você obtém o URL do servidor de relatório do administrador do servidor de relatório.  
  
#### <a name="to-specify-a-data-connection-from-a-list-of-shared-data-sources"></a>Para especificar uma conexão de dados de uma lista de fontes de dados compartilhadas  
  
1.  Na página **Escolher um conjunto de dados** , selecione **Criar um conjunto de dados**e clique em **Avançar**. A página **Escolher uma conexão com uma fonte de dados** é aberta.  
  
2.  Na lista de fontes de dados, selecione uma que você tenha permissão para acessar.  
  
3.  Para verificar se é possível se conectar à fonte de dados, clique em **Testar Conexão**. A mensagem "Conexão criada com êxito" será exibida. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  Clique em **Avançar**.  
  
     Se necessário, insira suas credenciais. Para salvar as credenciais localmente, selecione **Salvar senha com a conexão**. Se você não selecionar essa opção, deverá inserir credenciais sempre que executar o relatório  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-specify-a-data-connection-by-browsing-to-a-shared-data-source-on-a-report-server"></a>Para especificar uma conexão de dados navegando até uma fonte de dados compartilhada em um servidor de relatório  
  
1.  Na página **Escolher um conjunto de dados** , selecione **Criar um conjunto de dados**e clique em **Avançar**. A página **Escolher uma conexão com uma fonte de dados** é aberta.  
  
2.  Clique em **Procurar**. A caixa de diálogo **Selecionar Fonte de Dados** é aberta.  
  
3.  Na lista suspensa **Examinar** , selecione **Sites e Servidores Recentes**. No painel da fonte de dados, clique na URL do servidor e em **Abrir**.  
  
     A lista de fontes de dados ou modelos é exibida.  
  
4.  Como alternativa, em **Nome**, digite a URL do servidor de relatório. Clique em **Abrir**.  
  
     O Construtor de Relatórios é conectado ao servidor de relatório e carrega as fontes de dados disponíveis na pasta raiz.  
  
5.  Navegue até uma pasta que contém uma fonte de dados à qual você tenha permissões suficientes para se conectar, selecione-a e clique em **Abrir**.  
  
     Você voltará à página **Escolher uma conexão com uma fonte de dados** .  
  
6.  Para verificar se é possível se conectar à fonte de dados, clique em **Testar Conexão**.  
  
     A mensagem "Conexão criada com êxito" será exibida. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Clique em **Avançar**.  
  
8.  Se for solicitado que você informe um nome de usuário e uma senha, insira suas credenciais. Para salvar as credenciais localmente, selecione **Salvar senha com a conexão**.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Tutoriais do &#40;construtor de relatórios&#41;](report-builder-tutorials.md)  
  
  
