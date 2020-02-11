---
title: Visão geral de segurança (mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services - data mining], about security
ms.assetid: 387bde00-bcf3-4612-b27b-f9f608dbf71e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c55224b5590d23008de8b6caef7f120748f232bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082902"
---
# <a name="security-overview-data-mining"></a>Visão geral de segurança (mineração de dados)
  O processo de proteção [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ocorre em vários níveis. É necessário proteger cada instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e suas fontes de dados para garantir que somente os usuários autorizados tenham permissões de leitura ou de leitura/gravação nas dimensões, células, modelos de mineração e fontes de dados selecionadas. Você também tem que proteger as fontes de dados subjacentes para impedir que usuários não autorizados comprometam de modo mal-intencionado as informações de negócios confidenciais. O processo de proteção de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é descrito nos tópicos a seguir.  
  
##  <a name="bkmk_Architecture"></a>Arquitetura de segurança  
 Veja os seguintes recursos para saber sobre a arquitetura de segurança básica de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], incluindo como o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa a autenticação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para autenticar o acesso do usuário.  
  
-   [Funções de segurança &#40;Analysis Services de dados multidimensionais&#41;](../multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
-   [Propriedades de segurança](../server-properties/security-properties.md)  
  
-   [Configurar contas de serviço &#40;Analysis Services&#41;](../instances/configure-service-accounts-analysis-services.md)  
  
-   [Autorizar o acesso a objetos e operações &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_Logon"></a>Configurando a conta de logon para Analysis Services  
 É necessário selecionar uma conta de logon apropriada para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e especificar as permissões para essa conta. Verifique se a conta de logon do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tem apenas as permissões necessárias para executar as tarefas obrigatórias, incluindo as permissões adequadas para as fontes de dados subjacentes.  
  
 Para a mineração de dados, você precisa de um conjunto de permissões diferente para criar e processar modelos daquele necessário para exibir ou consultar os modelos. Fazer previsões em um modelo é um tipo de consulta e não requer permissões administrativas.  
  
##  <a name="bkmk_Instance"></a>Protegendo uma instância de Analysis Services  
 Em seguida, é necessário proteger o computador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , o sistema operacional Windows no computador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , o próprio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e as fontes de dados usadas pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
##  <a name="bkmk_Access"></a>Configurando o acesso ao Analysis Services  
 Quando você configura e define os usuários autorizados para uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], é necessário determinar quais usuários também devem ter permissão para administrar objetos de bancos de dados específicos, que os usuários podem exibir a definição de objetos ou procurar os modelos e que podem acessar fontes de dados diretamente.  
  
##  <a name="bkmk_DMspecial"></a>Considerações especiais para mineração de dados  
 Para permitir que um analista ou desenvolvedor crie e teste modelos de mineração de dados, você deve atribuir a esse analista ou desenvolvedor permissões administrativas no banco de dados em que os modelos de mineração estão armazenados. Em virtude disso, o analista ou desenvolvedor de mineração de dados pode criar ou excluir outros objetos não relacionados à mineração de dados, inclusive objetos de mineração de dados que foram criados e estão sendo utilizados por outros analistas ou desenvolvedores, ou objetos OLAP não incluídos na solução de mineração de dados.  
  
 Da mesma forma, quando você cria uma solução para mineração de dados, precisa equilibrar as necessidades do analista ou desenvolvedor para desenvolver, testar e ajustar modelos, em relação às necessidades de outros usuários, e adotar medidas para proteger os objetos de banco de dados existentes. Uma abordagem possível é criar um banco de dados separado dedicado à mineração de dados ou criar bancos de dados separados para cada analista.  
  
 Embora a criação de modelos exija o nível mais alto de permissões, você pode controlar o acesso do usuário aos modelos de mineração de dados para outras operações, como processamento, procura ou consulta, usando a segurança com base na função. Quando você cria uma função, define permissões que são específicas para objetos de mineração de dados. Qualquer usuário que seja um membro de uma função tem todas as permissões associadas a essa função automaticamente.  
  
 Além disso, modelos de mineração de dados frequentemente referenciam fontes de dados que contêm informações confidencial. Se a estrutura e o modelo de mineração tiverem sido configurados para permitir que os usuários detalhem do modelo para os dados na estrutura, você deve tomar precauções para mascarar informações confidenciais ou limitar os usuários que têm acesso aos dados subjacentes.  
  
 Se você usar pacotes de Integration Services para limpar dados, atualizar modelos de mineração ou fazer previsões, será necessário assegurar que o serviço Integration Services tenha as permissões apropriadas no banco de dados em que o modelo está armazenado e permissões apropriadas na fonte de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções e permissões &#40;Analysis Services&#41;](../multidimensional-models/roles-and-permissions-analysis-services.md)  
  
  
