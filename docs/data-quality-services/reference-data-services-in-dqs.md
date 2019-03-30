---
title: Serviços de dados de referência no DQS | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ef217717-6d05-443e-af26-44dc745a349d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 35ba90efe3233c34f710dda0e35b7108352df421
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658200"
---
# <a name="reference-data-services-in-dqs"></a>Serviços de Dados de Referência no DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Os dados de referência se referem a um conjunto exato e completo de dados relacionados ou globais categorizados (além dos limites de uma empresa) que estão disponíveis para domínios públicos confiáveis ou de provedores de conteúdo comercial premium.  
  
 O recurso Serviço de Dados de Referência no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) permite a você assinar provedores de dados de referência de terceiros e limpar facilmente e enriquecer os dados empresariais validando-os em relação aos dados de alta qualidade. Você pode usar serviços dos principais provedores do Data Quality Services de dentro do DQS para padronizar, corrigir ou enriquecer seus dados durante o processo de limpeza. Por exemplo, você pode usar uma lista de códigos de área ou CEPs em relação aos dados de referência para validar endereços de seus clientes.  
  
 O recurso Serviço de Dados de Referência tem os seguintes benefícios:  
  
-   Os dados de referência permitem que você assegure a qualidade dos dados comparando-os com os dados garantidos por outra empresa.  
  
-   O processo de dados de referência é incorporado na criação da base de dados de conhecimento do DQS e um projeto de qualidade de dados, permitindo a você instituir um processo de qualidade de dados abrangente.  
  
-   Oferece suporte ao uso de dados de referência do Windows Azure Marketplace, bem como diretamente de provedores de dados de referência de terceiros.  
  
##  <a name="Marketplace"></a> Usando dados de referência do Windows Azure Marketplace  
 O DQS oferece suporte ao uso de dados de referência do Windows Azure Marketplace para permitir que os provedores de conteúdo forneçam serviços de dados de referência por meio do Marketplace. O Marketplace é um serviço da Microsoft que fornece um único canal de mercado e entrega para dados e aplicativos de alta qualidade como serviços em nuvem. Para obter mais informações sobre o Marketplace, consulte [Saiba mais sobre o Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/about) (https://azuremarketplace.microsoft.com/about).
  
 A integração consistente entre o Marketplace e o DQS simplifica as etapas associadas à descoberta, exploração e aquisição de informações para projetos de qualidade de dados de dentro do DQS. Os dados são consumidos do DQS e ajudam os usuários do DQS na obtenção de alta qualidade de dados reunindo o DQS, o Marketplace e provedores de serviço de dados de referência de uma forma inovadora.  
  
 Para usar dados de referência do Marketplace no DQS para a atividade de limpeza, você deve ter uma chave de conta válida no Marketplace. A criação de uma chave de conta do Marketplace é gratuita e você pagará apenas se assinar os conjuntos de dados pagos. A assinatura e o uso de conjuntos de dados gratuitos não são cobrados. Para obter informações detalhadas sobre como criar uma chave de conta do Marketplace, consulte [Criar sua conta](https://go.microsoft.com/fwlink/?LinkId=212936) (https://go.microsoft.com/fwlink/?LinkId=212936).  
  
 Além disso, você pode executar as seguintes atividades do Marketplace de dentro do DQS:  
  
-   Procure conjuntos de dados no Marketplace.  
  
-   Crie uma chave de conta do Marketplace.  
  
-   Gerencie seus detalhes de conta do Marketplace como chaves de conta e assinaturas para provedores de dados.  
  
 Você pode executar essas atividades na guia **Dados de Referência** da tela **Configuração** no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
##  <a name="Direct"></a> Usando dados de referência diretamente de provedores de dados de referência de terceiros  
 Se você não estiver conectado à Internet e, portanto, não puder usar o Marketplace, o DQS também dará suporte à conexão direta com provedores de dados disponíveis na rede da sua organização. Para usar dados de referência de provedores de dados de referência de terceiros online diretos, você tem que criar um registro para o provedor de dados no DQS.  
  
##  <a name="HowToCleanse"></a> Como limpar dados usando dados de referência  
 Limpar seus dados no DQS usando dados de referência inclui as três seguintes etapas:  
  
1.  **Configurar os detalhes do provedor de dados de referência no DQS**: antes de usar dados de referência no DQS, é necessário configurar detalhes do serviço de dados de referência no DQS.  
  
    1.  Se você estiver usando o Marketplace, forneça uma chave de conta do Marketplace válida, vá para o [serviços de dados](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=data-services) categoria de dados no Marketplace e assine os provedores necessários.  
  
    2.  Se você estiver usando um provedor de dados de referência online direto, deverá adicionar detalhes desse provedor ao DQS antes de usá-lo.  
  
     Configurar os detalhes do provedor de dados de referência no DQS é uma atividade única para um provedor de dados específico. Somente administradores do DQS podem definir configurações de dados de referência no DQS.  
  
2.  **Mapear um domínio/domínio composto em uma base de dados de conhecimento para o serviço de dados de referência**: Mapear um domínio/domínio composto para o serviço de dados de referência adequado assinado/adicionado na etapa 1.  
  
3.  **Usar os domínios mapeados para a atividade de limpeza em um projeto de qualidade de dados**: ao criar um projeto de qualidade de dados para a atividade de **Limpeza**, selecione a base de dados de conhecimento que contém domínios/domínios compostos mapeados com serviços de dados de referência na etapa 2 e execute a atividade de limpeza.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como configurar o DQS para usar serviços de dados de referência do Marketplace ou provedores de dados online de terceiros diretos.|[Configurar DQS para usar dados de referência](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|Descreve como mapear um domínio/domínio composto em uma base de dados de conhecimento para um serviço de dados de referência.|[Anexar domínio ou domínio de composição para dados de referência](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|Descreve como limpar dados usando um serviço de dados de referência.|[Limpar dados usando o conhecimento &#40;externo&#41; dos dados de referência](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md)|  
  
  
