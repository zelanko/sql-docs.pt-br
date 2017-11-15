---
title: "Conectar ao Mecanismo de Banco de Dados do Servidor (página Propriedades da Conexão) | Microsoft Docs"
ms.custom: 
ms.date: 08/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttoce.connectionproperties.f1
- sql13.swb.connecttosqlserver.connectionproperties.f1
ms.assetid: edc1143c-6a47-4b02-92ab-441bdea8ea8a
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 92c974ad90689a01d4155610b71babc7df7765d3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="connect-to-server-connection-properties-page-database-engine"></a>Conectar ao Servidor (página Propriedades da Conexão) Mecanismo de Banco de Dados
Use esta guia para exibir ou especificar opções ao se conectar a uma emstância do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] ou registrar [!INCLUDE[ssDE](../../includes/ssde_md.md)] em **Servidores Registrados**. **Conectar** e **Opções** só são exibidas nesta caixa de diálogo ao conectar-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)]. **Testar** e **Salvar** só aparecem nesta caixa de diálogo durante o registro no [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
**Conectar ao banco de dados**  
Selecione um banco de dados com o qual deseja se conectar na lista. Ao selecionar **<default>**, você será conectado ao banco de dados padrão do servidor. Se você selecionar **<Browse server>**, poderá procurar no servidor o banco de dados ao qual se conectar.  
  
Ao conectar-se a uma instância do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] por meio do [!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)], você deve usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e especificar um banco de dados na caixa de diálogo **Conectar ao Servidor** , na guia **Propriedades da Conexão** . Verifique se você marcou a caixa de seleção **Criptografar conexão** .  
  
Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] conecta-se ao **mestre**. Ao conectar-se ao [!INCLUDE[ssSDS](../../includes/sssds_md.md)], se você especificar um banco de dados de usuário, somente esse banco de dados e seus objetos serão exibidos no Pesquisador de Objetos. Se você se conectar ao **mestre**, todos os bancos de dados serão exibidos. Para obter mais informações, consulte [Visão geral do banco de dados SQL do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
**Protocolo de rede**  
Selecione um protocolo na lista. Os protocolos de cliente disponíveis são configurados usando a configuração de rede do cliente no gerenciamento do computador.  
  
**Tamanho do pacote de rede**  
Digite o tamanho dos pacotes de rede a serem enviados. O padrão é 4096 bytes.  
  
**Tempo limite da conexão**  
Insira o número de segundos a esperar que uma conexão seja estabelecida antes do tempo expirar. O valor padrão é 15 segundos.  
  
**Tempo limite de execução**  
Digite o tempo em segundos que se deve esperar antes que a execução de uma tarefa seja concluída no servidor. O valor padrão é zero segundo, o que indica que não há nenhum tempo limite.  
  
**Criptografar conexão**  
Força a criptografia da conexão.  
  
**Usar cor personalizada**  
Selecione para especificar a cor do plano de fundo para a barra de status em uma janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde_md.md)] . Para especificar a cor, clique em **Selecionar**. Na caixa de diálogo **Cor** , selecione uma cor predefinida na grade **Cores básicas** ou clique em **Definir cores personalizadas** para definir e usar uma cor personalizada.  
  
-   Quando você especifica uma cor para uma entrada de servidor no painel **Pesquisador de Objetos** , aquela cor é usada quando você abre uma janela do Editor de Consultas. Para abrir uma janela do Editor de Consultas, clique com o botão direito do mouse em entrada de servidor e selecione **Nova Consulta**ou, quando o painel **Pesquisador de Objetos** estiver ativo e focalizado neste servidor, clique em **Nova Consulta** na barra de ferramentas.  
  
-   Quando você especifica uma cor para uma entrada de servidor no painel **Servidores Registrados** , aquela cor é usada quando você abre uma janela do Editor de Consultas. Para abrir uma janela do Editor de Consultas, clique com o botão direito do mouse em entrada de servidor e selecione **Nova Consulta**ou, quando o painel **Servidor Registrado** estiver ativo e focalizado neste servidor, clique em **Nova Consulta** na barra de ferramentas.  
  
-   No menu **Arquivo** , quando você clica em **Novo** e depois em **Consulta do Mecanismo do Banco de Dados**, a cor que você especifica na caixa de diálogo **Conectar ao Servidor** aplica-se àquela janela do Editor de Consultas.  
  
**ID de locatário ou nome de domínio do AD**  
Ao se conectar com a autenticação **Active Directory – Universal com MFA**, especifique o domínio de autenticação. Essa opção só está disponível ao usar o SSMS 17.2 ou posterior. 

**Redefinir Tudo**  
Substitua todos os valores de propriedade de conexão digitados manualmente por seus padrões.  
  
**Conectar**  
Tenta estabelecer uma conexão usando os valores listados.  
  
**Opções**  
Clique para alterar a caixa de diálogo e ocultar as opções de conexão de servidor adicionais, como lembrar a senha.  
  
**Testar**  
Ao registrar o [!INCLUDE[ssDE](../../includes/ssde_md.md)] em **Servidores Registrados**, clique para testar a conexão.  
  
**Salvar**  
Salve as configurações em **Servidores Registrados**.  
  
## <a name="see-also"></a>Consulte também  
[Caixa de diálogo Propriedades da conexão](../../ssms/f1-help/connection-properties-dialog-box.md)  
  
