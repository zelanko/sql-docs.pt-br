---
title: Conectar ao Mecanismo de Banco de Dados do Servidor (página Propriedades da Conexão) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttosqlserver.connectionproperties.f1
ms.assetid: edc1143c-6a47-4b02-92ab-441bdea8ea8a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30382bcb0c70fb985c88866602cb997988b88569
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70153747"
---
# <a name="connect-to-server-connection-properties-page-database-engine"></a>Conectar ao Servidor (página Propriedades da Conexão) Mecanismo de Banco de Dados
  Use esta guia para exibir ou especificar opções ao se conectar a uma emstância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ou registrar [!INCLUDE[ssDE](../../includes/ssde-md.md)] em **Servidores Registrados**. **** **As opções** conectar e somente aparecem nessa caixa de diálogo ao se conectar a uma instância [!INCLUDE[ssDE](../../includes/ssde-md.md)]do. **Test** e **Save** aparecem apenas nesta caixa de diálogo durante o registro [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="options"></a>Opções  
 **Conectar ao banco de dados**  
 Selecione um banco de dados com o qual deseja se conectar na lista. Se você selecionar ** \<>padrão **, você será conectado ao banco de dados padrão para o servidor. Se você selecionar ** \<procurar>de servidor **, poderá procurar o banco de dados ao qual se conectará o servidor.  
  
 Ao se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados por [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]meio do, você [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve usar a autenticação do e especificar um banco de dados na caixa de diálogo **conectar ao servidor** , na guia **Propriedades da conexão** . Marque a caixa de seleção **criptografar conexão** .  
  
 Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conecta-se ao **mestre**. Se você especificar um banco de dados de usuário, consultará somente esse banco de dados e seus objetos no Pesquisador de Objetos. Se você se conectar ao **mestre**, poderá ver todos os bancos de dados. Para obter mais informações, consulte [visão geral do banco de dados SQL do Azure](/azure/sql-database/sql-database-technical-overview).  
  
 **Protocolo de rede**  
 Selecione um protocolo na lista. Os protocolos cliente disponíveis são aqueles que você configurou usando a Configuração de Rede Cliente no Gerenciamento do Computador.  
  
 **Tamanho do pacote de rede**  
 Digite o tamanho dos pacotes de rede a serem enviados. O padrão é 4096 bytes.  
  
 **Tempo limite da conexão**  
 Insira o número de segundos de espera para que uma conexão seja estabelecida antes de atingir o tempo limite. O valor padrão é 15 segundos.  
  
 **Tempo limite de execução**  
 Digite o tempo em segundos que se deve esperar antes que a execução de uma tarefa seja concluída no servidor. O valor padrão é zero segundo, o que indica que não há nenhum tempo limite.  
  
 **Criptografar conexão**  
 Força a criptografia da conexão.  
  
 **Usar cor personalizada**  
 Selecione para especificar a cor do plano de fundo para a barra de status em uma janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Para especificar a cor, clique em **Selecionar**. Na caixa de diálogo **Cor** , selecione uma cor predefinida na grade **Cores básicas** ou clique em **Definir cores personalizadas** para definir e usar uma cor personalizada.  
  
-   Quando você especifica uma cor para uma entrada de servidor no painel **Pesquisador de Objetos** , aquela cor é usada quando você abre uma janela do Editor de Consultas. Para abrir uma janela do Editor de Consultas, clique com o botão direito do mouse em entrada de servidor e selecione **Nova Consulta**ou, quando o painel **Pesquisador de Objetos** estiver ativo e focalizado neste servidor, clique em **Nova Consulta** na barra de ferramentas.  
  
-   Quando você especifica uma cor para uma entrada de servidor no painel **Servidores Registrados** , aquela cor é usada quando você abre uma janela do Editor de Consultas. Para abrir uma janela do Editor de Consultas, clique com o botão direito do mouse em entrada de servidor e selecione **Nova Consulta**ou, quando o painel **Servidor Registrado** estiver ativo e focalizado neste servidor, clique em **Nova Consulta** na barra de ferramentas.  
  
-   No menu **Arquivo** , quando você clica em **Novo** e depois em **Consulta do Mecanismo do Banco de Dados**, a cor que você especifica na caixa de diálogo **Conectar ao Servidor** aplica-se àquela janela do Editor de Consultas.  
  
 **Redefinir tudo**  
 Substitua todos os valores de propriedade de conexão digitados manualmente por seus padrões.  
  
 **Connect**  
 Tenta estabelecer uma conexão usando os valores listados.  
  
 **Opções**  
 Clique para alterar a caixa de diálogo e ocultar as opções de conexão de servidor adicionais, como lembrar a senha.  
  
 **Testar**  
 Ao registrar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] em **Servidores Registrados**, clique para testar a conexão.  
  
 **Salvar**  
 Salve as configurações em **Servidores Registrados**.  
  
## <a name="see-also"></a>Consulte Também  
 [caixa de diálogo Propriedades da conexão](../../database-engine/connection-properties-dialog-box.md)  
  
  
