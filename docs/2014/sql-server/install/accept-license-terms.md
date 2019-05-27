---
title: Aceite os termos de licença | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- license terms
helpviewer_keywords:
- Registration Information page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Registration Information page
ms.assetid: 08dd739d-5817-4418-bcff-74ab7f8bbd33
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 99418b11eecdb3077e3def746eae56e43bab2d60
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096837"
---
# <a name="accept-license-terms"></a>Aceitar termos de licença
  Use a página **Aceitar Termos de Licença** do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para aceitar os termos da licença desta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Você pode imprimir o contrato de licença ou copiá-lo para a Área de transferência. Para continuar, aceite os termos da licença e clique em **Avançar**. Para fechar a instalação, clique em **Cancelar**.  
  
## <a name="customer-experience-improvement-program-ceip"></a>Programa de Aperfeiçoamento da Experiência do Usuário (CEIP)  
 Se você habilitar os relatórios CEIP, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será configurado para enviar, periodicamente, um relatório para a [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Relatórios incluem informações sobre sua configuração de hardware e como você usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os componentes. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] usará dados de uso de recurso para melhorar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] monitorados por esse recurso incluem:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Replicação  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instalação  
  
 As informações sobre o uso de recursos são enviadas para a [!INCLUDE[msCoName](../../includes/msconame-md.md)], onde são armazenadas com acesso limitado.  
  
 Para desabilitar os relatórios do CEIP (Programa de Aperfeiçoamento da Experiência do Usuário) após a conclusão da Instalação, use a ferramenta **Relatório de Erro e Uso** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no menu **Ferramentas de Configuração** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para ações de Instalação como instalação, atualização, reparo, e assim por diante, as informações são coletadas e carregadas somente durante a execução do programa de instalação  
  
 Para todos os outros componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , as informações são coletadas uma vez por dia para todas as instâncias habilitadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, a hora de coleta é meia-noite para minimizar a carga no servidor. Se quiser alterar a hora de coleta, poderá editar manualmente a chave do registro que controla isso. Cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem sua própria chave do Registro:  
  
 HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<INSTANCEID>\CPE\TimeofReporting  
  
 O valor dessa chave do Registro contém a hora de coleta como o número de minutos a partir de 00h:00 (meia-noite) para executar. Por exemplo, um valor igual a 60 executará a coleta à 1:00 a.m. e um valor igual a 1200 executará a coleta às 8:00 p.m., e assim por diante.  
  
## <a name="error-reporting"></a>Relatório de Erros  
 Use a página **Configurações do Relatório de Erro e Uso** do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar a funcionalidade de relatório de erro e uso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="options"></a>Opções  
 Por padrão, a coleta de dados sobre Uso de Recursos e o Relatório de Erros ficam habilitados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e seus componentes no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Relatório de Erros  
 Se você habilitar o recurso Relatório de Erros, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será configurado para enviar, automaticamente, um relatório para a [!INCLUDE[msCoName](../../includes/msconame-md.md)] caso um erro fatal ocorra em qualquer um dos seguintes componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Replicação  
  
 A [!INCLUDE[msCoName](../../includes/msconame-md.md)] usa relatórios de erros para melhorar a funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e trata todas as informações como confidenciais.  
  
 As informações sobre erros são enviadas através de uma conexão segura (https) para a [!INCLUDE[msCoName](../../includes/msconame-md.md)], onde são armazenadas com acesso limitado. Como alternativa, os relatórios de erros podem ser enviados para seu próprio servidor corporativo de relatório de erros.  
  
 Os relatórios de erros contêm as seguintes informações:  
  
-   A condição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando ocorreu o problema.  
  
-   A versão do sistema operacional e as informações de hardware.  
  
-   Sua identificação digital do produto, que não é usado para identificar sua licença.  
  
-   O endereço IP da rede do seu computador ou do servidor proxy.  
  
-   Informações de memória ou do(s) arquivo(s) do processo que causou o erro.  
  
 A [!INCLUDE[msCoName](../../includes/msconame-md.md)] não coleta seus arquivos nem seu nome, endereço, endereço de email ou qualquer outro formulário com informações pessoais intencionalmente. Entretanto, o relatório de erros pode conter informações pessoais da memória ou dos arquivos do processo que causou o erro. Apesar de essas informações poderem ser potencialmente usadas para determinar sua identidade, a [!INCLUDE[msCoName](../../includes/msconame-md.md)] não usa essas informações com esse propósito.  
  
 Para obter mais informações sobre a política de privacidade e de coleta de dados da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Microsoft SQL Server Privacy Statement](../../../2014/getting-started/microsoft-sql-server-privacy-statement.md).  
  
 Se você habilitar Relatório de Erros e um erro fatal ocorrer, poderá ver uma resposta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] no log de eventos do Windows que apontará para um artigo específico na Base de Dados de Conhecimento [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Para desabilitar os recursos de relatório de erro ou de uso para todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de seus componentes, depois de finalizar a Instalação, vá para a caixa de diálogo **Configurações do Relatório de Erro e Uso** e desmarque a caixa de seleção **Uso de Recursos**. Se a caixa **Relatório de Erros** estiver habilitada para vários componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e componentes compartilhados), você poderá desabilitar essa opção para cada instância do componente, bem como para os componentes compartilhados listados como **Outros**.  
  
## <a name="see-also"></a>Consulte também  
 [Sobre os termos de licença do SQL Server](../../../2014/getting-started/about-the-sql-server-license-terms.md)  
  
  
