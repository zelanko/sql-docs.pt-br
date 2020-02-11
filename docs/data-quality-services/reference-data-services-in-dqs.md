---
title: Serviços de Dados de Referência no DQS
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ef217717-6d05-443e-af26-44dc745a349d
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 6d3c4f15dcb62e36918c81baa5f2bd40c38b7c6a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75244144"
---
# <a name="reference-data-services-in-dqs"></a>Serviços de Dados de Referência no DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Os dados de referência se referem a um conjunto exato e completo de dados relacionados ou globais categorizados (além dos limites de uma empresa) que estão disponíveis para domínios públicos confiáveis ou de provedores de conteúdo comercial premium.  
  
 O recurso Serviço de Dados de Referência no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) permite a você assinar provedores de dados de referência de terceiros e limpar facilmente e enriquecer os dados empresariais validando-os em relação aos dados de alta qualidade. Você pode usar serviços dos principais provedores do Data Quality Services de dentro do DQS para padronizar, corrigir ou enriquecer seus dados durante o processo de limpeza. Por exemplo, você pode usar uma lista de códigos de área ou CEPs em relação aos dados de referência para validar endereços de seus clientes.  
  
 O recurso Serviço de Dados de Referência tem os seguintes benefícios:  
  
-   Os dados de referência permitem que você assegure a qualidade dos dados comparando-os com os dados garantidos por outra empresa.  
  
-   O processo de dados de referência é incorporado na criação da base de dados de conhecimento do DQS e um projeto de qualidade de dados, permitindo a você instituir um processo de qualidade de dados abrangente.  
  
-   Dá suporte ao uso de dados de referência do Azure Marketplace, bem como diretamente de provedores de dados de referência de terceiros.  
  
##  <a name="Marketplace"></a>Usando dados de referência do Azure Marketplace  
 O DQS dá suporte ao uso de dados de referência do Azure Marketplace para habilitar os provedores de conteúdo a fornecer serviços de dados de referência por meio do Marketplace. O Marketplace é um serviço da Microsoft que fornece um único canal de mercado e entrega para dados e aplicativos de alta qualidade como serviços em nuvem. Para obter mais informações sobre o Marketplace, consulte Saiba maishttps://azuremarketplace.microsoft.com/about) [sobre Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/about) (.
  
 A integração consistente entre o Marketplace e o DQS simplifica as etapas associadas à descoberta, exploração e aquisição de informações para projetos de qualidade de dados de dentro do DQS. Os dados são consumidos do DQS e ajudam os usuários do DQS na obtenção de alta qualidade de dados reunindo o DQS, o Marketplace e provedores de serviço de dados de referência de uma forma inovadora.  
  
 Para usar dados de referência do Marketplace no DQS para a atividade de limpeza, você deve ter uma chave de conta válida no Marketplace. A criação de uma chave de conta do Marketplace é gratuita e você pagará apenas se assinar os conjuntos de dados pagos. A assinatura e o uso de conjuntos de dados gratuitos não são cobrados. Para obter informações detalhadas sobre como criar uma chave de conta do Marketplace, consultehttps://go.microsoft.com/fwlink/?LinkId=212936) [criar sua conta](https://go.microsoft.com/fwlink/?LinkId=212936) (.  
  
 Além disso, você pode executar as seguintes atividades do Marketplace de dentro do DQS:  
  
-   Procure conjuntos de dados no Marketplace.  
  
-   Crie uma chave de conta do Marketplace.  
  
-   Gerencie seus detalhes de conta do Marketplace como chaves de conta e assinaturas para provedores de dados.  
  
 Você pode executar essas atividades na guia **Dados de Referência** da tela **Configuração** no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
##  <a name="Direct"></a>Usando dados de referência diretamente dos provedores de dados de referência de terceiros  
 Se você não estiver conectado à Internet e, portanto, não puder usar o Marketplace, o DQS também dará suporte à conexão direta com provedores de dados disponíveis na rede da sua organização. Para usar dados de referência de provedores de dados de referência de terceiros online diretos, você tem que criar um registro para o provedor de dados no DQS.  
  
##  <a name="HowToCleanse"></a>Como limpar dados usando os dados de referência  
 Limpar seus dados no DQS usando dados de referência inclui as três seguintes etapas:  
  
1.  **Configurando os detalhes do provedor de dados de referência no DQS**: antes de poder usar dados de referência no DQS, você deve configurar detalhes do serviço de dados de referência no DQS.  
  
    1.  Se você estiver usando o Marketplace, forneça uma chave de conta válida do Marketplace, navegue até a categoria de dados [dos serviços de dados](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=data-services) no Marketplace e assine os provedores necessários.  
  
    2.  Se você estiver usando um provedor de dados de referência online direto, deverá adicionar detalhes desse provedor ao DQS antes de usá-lo.  
  
     Configurar os detalhes do provedor de dados de referência no DQS é uma atividade única para um provedor de dados específico. Somente administradores do DQS podem definir configurações de dados de referência no DQS.  
  
2.  **Mapear um domínio/domínio composto em uma base de conhecimento para o serviço de dados de referência**: mapeie um domínio/domínios de composição para o serviço de dados de referência apropriado assinado/adicionado na etapa 1.  
  
3.  **Use os domínios mapeados para a atividade de limpeza em um projeto de qualidade de dados**: ao criar um projeto de qualidade de dados para a atividade de **limpeza** , selecione a base de dados de conhecimento que contém domínios/domínios compostos mapeados com serviços de dados de referência na etapa 2 e execute a atividade de limpeza.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como configurar o DQS para usar serviços de dados de referência do Marketplace ou provedores de dados online de terceiros diretos.|[Configurar DQS para usar dados de referência](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|Descreve como mapear um domínio/domínio composto em uma base de dados de conhecimento para um serviço de dados de referência.|[Anexar domínio ou domínio composto para dados de referência](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|Descreve como limpar dados usando um serviço de dados de referência.|[Limpar dados usando dados de referência &#40;conhecimento de&#41; externo](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md)|  
  
  
