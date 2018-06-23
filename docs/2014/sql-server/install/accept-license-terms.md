---
title: Aceite os termos de licença | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- license terms
helpviewer_keywords:
- Registration Information page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Registration Information page
ms.assetid: 08dd739d-5817-4418-bcff-74ab7f8bbd33
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 55d500b13cc3ab3c859474bb3050e29a7487f4a3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122976"
---
# <a name="accept-license-terms"></a>Aceitar termos de licença
  Use o **aceitar termos de licença** página do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de instalação para aceitar os termos de licença para esta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Você pode imprimir o contrato de licença ou copiá-lo para a Área de transferência. Para continuar, aceite os termos da licença e clique em **Avançar**. Para fechar a instalação, clique em **Cancelar**.  
  
## <a name="customer-experience-improvement-program-ceip"></a>Programa de Aperfeiçoamento da Experiência do Usuário (CEIP)  
 Se você habilitar os relatórios CEIP, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será configurado para enviar, periodicamente, um relatório para a [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Relatórios incluem informações sobre sua configuração de hardware e como você usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os componentes. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] usará dados de uso de recurso para melhorar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] monitorados por esse recurso incluem:  
  
-   O [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Replicação  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instalação  
  
 Informações sobre o uso de recursos são enviadas para [!INCLUDE[msCoName](../../includes/msconame-md.md)], onde são armazenadas com acesso limitado.  
  
 Para desabilitar os relatórios CEIP após a conclusão da instalação, use o  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relatório de erro e uso** ferramenta sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ferramentas de configuração** menu.  
  
 Para ações de Instalação como instalação, atualização, reparo, e assim por diante, as informações são coletadas e carregadas somente durante a execução do programa de instalação  
  
 Para todos os outros componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as informações são coletadas uma vez por dia para todas as instâncias habilitadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, a hora de coleta é meia-noite para minimizar a carga no servidor. Se quiser alterar a hora de coleta, poderá editar manualmente a chave do registro que controla isso. Cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem sua própria chave de registro:  
  
 HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<InstanceName>\.\< INSTANCEID > \CPE\TimeofReporting  
  
 O valor dessa chave do Registro contém a hora de coleta como o número de minutos a partir de 00h:00 (meia-noite) para executar. Por exemplo, um valor igual a 60 executará a coleta à 1:00 a.m. e um valor igual a 1200 executará a coleta às 8:00 p.m., e assim por diante.  
  
## <a name="error-reporting"></a>Relatório de Erros  
 Use o **configurações do relatório de uso e erro** página do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de instalação para habilitar o erro e uso para a funcionalidade de emissão de relatórios [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="options"></a>Opções  
 Por padrão, a coleta de dados de uso de recursos e recursos de relatório de erros estão desabilitados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e seus componentes no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Relatório de Erros  
 Se você habilitar o recurso relatório de erros, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para enviar um relatório para [!INCLUDE[msCoName](../../includes/msconame-md.md)] automaticamente se ocorrer um erro fatal em qualquer um dos seguintes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes:  
  
-   O [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Replicação  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] usa relatórios de erros para melhorar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funcionalidade e trata todas as informações como confidenciais.  
  
 As informações sobre erros são enviadas através de uma conexão segura (https) para a [!INCLUDE[msCoName](../../includes/msconame-md.md)], onde são armazenadas com acesso limitado. Como alternativa, os relatórios de erros podem ser enviados para seu próprio servidor corporativo de relatório de erros.  
  
 Os relatórios de erros contêm as seguintes informações:  
  
-   A condição de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando ocorreu o problema.  
  
-   A versão do sistema operacional e as informações de hardware.  
  
-   Sua identificação digital do produto, que não é usado para identificar sua licença.  
  
-   O endereço IP da rede do seu computador ou do servidor proxy.  
  
-   Informações de memória ou do(s) arquivo(s) do processo que causou o erro.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] não coleta intencionalmente seus arquivos, nome, endereço, endereço de email ou qualquer outra forma de informações pessoais. Entretanto, o relatório de erros pode conter informações pessoais da memória ou dos arquivos do processo que causou o erro. Apesar de essas informações poderem ser potencialmente usadas para determinar sua identidade, a [!INCLUDE[msCoName](../../includes/msconame-md.md)] não usa essas informações com esse propósito.  
  
 Para obter mais informações sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] privacidade e a política de coleta de dados, consulte [declaração de privacidade do Microsoft SQL Server](../../../2014/getting-started/microsoft-sql-server-privacy-statement.md).  
  
 Se você habilitar Relatório de Erros e um erro fatal ocorrer, poderá ver uma resposta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] no log de eventos do Windows que apontará para um artigo específico na Base de Dados de Conhecimento [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 Para desabilitar o relatório de erro ou de uso do recurso para todas as instâncias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e seus componentes após a conclusão da instalação, vá para o **configurações do relatório de uso e erro** caixa de diálogo e desmarque a caixa de seleção **uso de recursos** . Se **relatório de erros** está habilitada para vários componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e os componentes compartilhados) você pode desabilitar o relatório de erros para cada instância de um indivíduo componente, bem como os componentes compartilhados listados como **outros**.  
  
## <a name="see-also"></a>Consulte também  
 [Sobre os termos de licença do SQL Server](../../../2014/getting-started/about-the-sql-server-license-terms.md)  
  
  