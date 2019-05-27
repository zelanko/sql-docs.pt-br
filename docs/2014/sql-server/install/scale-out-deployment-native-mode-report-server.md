---
title: Escalar horizontalmente a implantação (servidor de relatório do modo nativo) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.scaleoutdeployment.F1
ms.assetid: 4df38294-6f9d-4b40-9f03-1f01c1f0700c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f26787441fb93253b9ca944c479f9cf480ba0745
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092427"
---
# <a name="scale-out-deployment-native-mode-report-server"></a>Implantação de expansão (modo nativo do Servidor de Relatório)
  Use a página **Implantação de Expansão** no Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para exibir o status de inicialização de uma implantação de expansão ou para unir um servidor de relatório a uma implantação de expansão. Uma *implantação de expansão* se refere a duas ou mais instâncias do servidor de relatório que compartilham um único banco de dados do servidor de relatório.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Um *servidor de relatório inicializado* descreve um servidor que pode criptografar e descriptografar dados confidenciais que estão armazenados em um banco de dados do servidor de relatório (credenciais armazenadas e cadeias de conexão são exemplos de dados criptografados que são armazenados no banco de dados). A inicialização do servidor de relatório é um requisito para as operações do servidor de relatório.  
  
 Uma *implantação de expansão* é usada nos seguintes cenários:  
  
-   Como um pré-requisito para o balanceamento de carga de vários servidores de relatório em um cluster de servidores. Antes de balancear a carga de vários servidores de relatório, primeiro é necessário configurá-los para compartilhar o mesmo banco de dados do servidor de relatório.  
  
-   Para segmentar aplicativos de servidor de relatório em diferentes computadores, usando um servidor para processamento de relatório interativo e um segundo servidor para processamento de relatório agendado. Neste cenário, cada instância do servidor processa diferentes tipos de solicitações para o mesmo conteúdo do servidor de relatório armazenado no banco de dados do servidor de relatório compartilhado.  
  
 Para configurar uma implantação de expansão, inicie com duas ou mais instâncias do servidor de relatório que estejam conectadas ao mesmo banco de dados do servidor de relatório. Depois que todas as instâncias estiverem instaladas, conecte-se ao primeiro servidor de relatório e use a página Implantação de Expansão para associar cada instância adicional. Apenas um servidor de relatório que já esteja inicializado para usar um banco de dados pode inicializar nós adicionais.  
  
 Para abrir essa página, inicie o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e selecione **Implantação de Expansão** no painel de navegação. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opções  
 **SQL Server Name**  
 Especifique o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda o banco de dados do servidor de relatório.  
  
 **Database Name**  
 Especifica o nome do banco de dados ao qual a instância do servidor de relatório está atualmente conectada.  
  
 **Modo de servidor**  
 Exibe o modo do servidor e do banco de dados. O modo do servidor é Nativo ou integrado do SharePoint. Os dois modos dão suporte a implantações de expansão.  
  
 **Servidor**  
 Mostra o nome do servidor de relatório. Na maioria dos casos, esse é o nome do computador no qual o servidor de relatório está instalado.  
  
 **Instância**  
 Mostra o nome da instância do servidor de relatório. As instâncias do servidor de relatório têm como base as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Status**  
 Indica se o servidor de relatório está inicializado ou aguardando para associar-se a uma implantação de expansão:  
  
-   Para um servidor de relatório autônomo que não faça parte de uma implantação de expansão, essa página mostra que a instância do servidor de relatório está inicializada com relação a seu banco de dados do servidor de relatório dedicado. O status é definido como **Associado**.  
  
-   Para um servidor de relatório que esteja aguardando para associar-se a uma implantação de expansão, essa página contém valores vazios para Servidor, Instância e Status. Um servidor de relatório estará aguardando para associar-se a uma implantação de expansão se você selecionou um banco de dados de servidor de relatório existente que já seja usado por outra instância do servidor de relatório. Uma mensagem nessa página o instrui a conectar-se a um servidor de relatório que já esteja associado ao farm. Para concluir essa solicitação, clique em **Conectar**, selecione um servidor de relatório que já esteja inicializado para usar o banco de dados do servidor de relatório, clique em **Implantação de Expansão**, selecione a instância do servidor de relatório que está **Aguardando para Associar**e clique em **Inicializar**.  
  
-   Para um servidor de relatório que atualmente faça parte de uma implantação de expansão, essa página mostra o status de inicialização de todas as instâncias do servidor de relatório que compartilham o mesmo banco de dados do servidor de relatório. Ao exibir o status de uma implantação de expansão, não importa a qual servidor você está conectado. As informações de status são relatadas identicamente para todos os nós na implantação de expansão.  
  
     Para um servidor de relatório que já faça parte de uma implantação de expansão, você pode usar essa página para adicionar ou remover nós.  
  
 **inicializar**  
 Clique em **Inicializar** para adicionar um servidor de relatório à implantação de expansão. Esta etapa configura um servidor de relatório para usar uma chave simétrica em um banco de dados do servidor de relatório compartilhado. Você pode usar **Inicializar** para adicionar uma instância do servidor de relatório a uma implantação de expansão ou para solucionar um problema de migração ou instalação.  
  
 Uma instância de servidor de relatório estará disponível somente se você configurou anteriormente uma conexão com o banco de dados do servidor de relatório compartilhado. Além disso, é necessário executar a inicialização a partir de um servidor de relatório que já esteja inicializado para usar o banco de dados do servidor de relatório.  
  
 **Remover**  
 Clique em **Remover** para remover do banco de dados do servidor de relatório as chaves de criptografia da instância selecionada do servidor de relatório. Você pode remover chaves para remover um servidor de relatório de uma implantação de expansão ou para solucionar um problema de migração ou instalação. Com esta opção, apenas as chaves de criptografia da instância especificada do servidor de relatório são removidas. Os dados criptografados do banco de dados do servidor de relatório não são afetados.  
  
 Como precaução, certifique-se de criar uma cópia de backup da chave simétrica antes de removê-la. Depois de remover as chaves de criptografia do último servidor de relatório na lista, introduza novos requisitos para qualquer inicialização subsequente do servidor de relatório para esse banco de dados. O novo requisito consiste em que, depois de inicializar um servidor de relatório, você deve restaurar uma cópia de backup da chave simétrica. A restauração da chave simétrica será necessária se você deseja acessar os dados criptografados que estejam atualmente no banco de dados do servidor de relatório.  
  
 Se os dados criptografados não mais forem necessários ou se você não tiver uma cópia de backup da chave, você deverá excluir os dados criptografados. Para obter mais informações, consulte [chaves de criptografia &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md).  
  
## <a name="see-also"></a>Consulte também  
 [Inicializar um servidor de relatório &#40; Configuration Manager do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [Configurar uma implantação de expansão do servidor de relatório no modo nativo &#40;Gerenciador de configurações do SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
  
  
