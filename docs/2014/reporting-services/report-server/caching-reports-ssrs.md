---
title: Armazenando relatórios em cache (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- report processing [Reporting Services], caching
- cached instances [Reporting Services]
- refreshing cache
- cached reports [Reporting Services]
- preloading cache
- invalid cached reports [Reporting Services]
- performance [Reporting Services]
- expiration [Reporting Services]
- snapshots [Reporting Services], caching
ms.assetid: 146542c3-8efd-4b89-a8d8-77d22896630e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 58785d54954278d2dcb839ef3e707859682a9d37
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66104107"
---
# <a name="caching-reports-ssrs"></a>Armazenando relatórios em cache (SSRS)
  Um servidor de relatório pode armazenar em cache uma cópia de um relatório processado e devolvê-la quando um usuário abrir o relatório. Para o usuário, a única evidência disponível indicativa de que o relatório é uma cópia armazenada em cache são os dados de data e hora de processamento do relatório. Se a data ou a hora não for atual e o relatório não for um instantâneo, ele terá sido recuperado do cache.  
  
 O armazenamento em cache pode diminuir o tempo necessário para recuperar um relatório, caso ele seja grande ou acessado frequentemente. Se o servidor for reinicializado, todas as instâncias armazenadas em cache serão reintegradas quando o serviço da Web do Servidor de Relatório ficar online.  
  
 O armazenamento em cache é uma técnica de aprimoramento de desempenho. O conteúdo do cache é volátil e pode mudar à medida que relatórios são adicionados, substituídos ou removidos. Se for necessária uma estratégia mais previsível de armazenamento em cache, você deverá criar um instantâneo de relatório. Para obter mais informações, consulte [Definir as propriedades do processamento de relatórios](set-report-processing-properties.md).  
  
> [!NOTE]  
>  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] armazena arquivos temporários em um banco de dados para dar suporte a sessões de usuário e processamento de relatório. Esses arquivos são armazenados em cache para uso interno e para oferecer suporte a uma experiência de visualização consistente durante uma única sessão de navegador. Para obter mais informações sobre como os arquivos temporários de uso interno são armazenados em cache, consulte [Banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](report-server-database-ssrs-native-mode.md).  
  
## <a name="cached-instances"></a>Instâncias armazenadas em cache  
 Uma instância armazenada em cache de um relatório baseia-se no formato intermediário de um relatório. O servidor de relatório geralmente armazena em cache uma instância de um relatório com base no nome de relatório. No entanto, se um relatório puder conter dados diferentes com base nos parâmetros de consulta, várias versões do relatório poderão ser armazenadas em cache em um determinado momento. Por exemplo, suponha que você tem um relatório com parâmetros que assume um código de região como um valor de parâmetro. Se quatro usuários diferentes especificarem quatro códigos de região exclusivos, serão criadas quatro cópias armazenadas em cache.  
  
 O primeiro usuário que executar o relatório com um único código de região cria um relatório armazenado em cache que contém dados para essa região. Usuários subsequentes que solicitam o relatório usando o mesmo código de região obtêm a cópia armazenada em cache.  
  
 Nem todos os relatórios podem ser armazenados em cache. Se um relatório incluir dados que dependem do usuário, ele solicitará aos usuários as credenciais ou usará a Autenticação do Windows, ele não poderá ser armazenado em cache.  
  
## <a name="refreshing-the-cache"></a>Atualizando o cache  
 Um relatório armazenado em cache é substituído por uma versão mais nova quando um usuário o seleciona após a expiração da cópia anteriormente armazenada em cache. Os relatórios configurados para execução como instâncias armazenadas em cache são removidos do cache em intervalos com base nas configurações de expiração. Você pode definir a expiração de um relatório em minutos ou em um horário agendado, conforme determinado pela condição de necessidade imediata dos dados. Não é possível excluir relatórios do cache diretamente, a menos que você use a API SOAP.  
  
 Para configurar a expiração de cache, você pode usar uma agenda compartilhada ou específica do relatório. Se você usar uma agenda compartilhada e ela sofrer pausa subsequente, o cache não expirará enquanto a agenda estiver inoperante. Se a agenda compartilhada for excluída em seguida, terá uma cópia salva como agenda específica do relatório.  
  
 Se uma agenda expirar ou se o mecanismo de agendamento não estiver disponível em uma data de expiração de cache, o servidor de relatório executará um relatório dinâmico até que as operações agendadas possam ser retomadas (estendendo a agenda ou iniciando o serviço de agendamento).  
  
## <a name="preloading-the-cache"></a>Pré-carregando o cache  
 Para melhorar o desempenho do servidor, você pode pré-carregar o cache. Você pode pré-carregar o cache com uma coleção de instâncias de relatório parametrizadas de duas maneiras:  
  
1.  Crie um plano de atualização de cache. Quando você cria um plano de atualização, pode especificar uma agenda para um único relatório ou pode especificar uma agenda compartilhada.  
  
2.  Crie uma assinatura controlada por dados que usa o Provedor de Entrega Nulo. Quando você especificar o Provedor de Entrega Nulo como método de entrega na assinatura, o servidor de relatório apontará o banco de dados do servidor de relatório como o destino de entrega e usará uma extensão de renderização especializada chamada de extensão de renderização nula. Em comparação com outras extensões de entrega, o Provedor de Entrega Nulo não tem configurações de entrega que podem ser configuradas por uma definição de assinatura.  
  
 Armazenar um relatório em cache é especialmente útil se você deseja armazenar em cache múltiplas instâncias de um relatório parametrizado, em que diferentes valores de parâmetro são usados para produzir diferentes instâncias de relatório. Observe que você só pode especificar parâmetros com base em consultas no relatório.  
  
 Ao especificar uma agenda ou criar uma assinatura controlada por dados, você agenda a frequência de entrega desses relatórios ao cache. Para que cópias novas sejam entregues ao cache, as cópias antigas devem ter expirado. Portanto, as propriedades de Execução do relatório devem ser configuradas para incluir as configurações de expiração de cache. A configuração de expiração deve ser consistente com a agenda de assinatura definida. Por exemplo, se você criar uma assinatura que é executada todas as noites, o cache também deverá expirar todas as noites antes do tempo de execução da assinatura. Se as propriedades de Execução não incluírem momentos de expiração, novas entregas serão desconsideradas. Para obter mais informações sobre planos de atualização de cache, consulte [Agendamentos](../subscriptions/schedules.md). Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades do processamento de relatórios](set-report-processing-properties.md). Para obter mais informações sobre o uso de assinaturas controladas por dados, consulte [Assinaturas controladas por dados](../subscriptions/data-driven-subscriptions.md).  
  
## <a name="conditions-that-cause-cache-expiration"></a>Condições que causam a expiração de cache  
 Um relatório armazenado em cache é invalidado em resposta aos seguintes eventos: a definição do relatório é modificada, os parâmetros do relatório são modificados, as credenciais de fonte de dados mudam ou as opções de execução do relatório mudam. Se você excluir um relatório armazenado em cache, a versão armazenada também será excluída.  
  
 Se um relatório não puder ser processado a partir de uma instância armazenada em cache por qualquer motivo (por exemplo, se os valores de parâmetro que um usuário especifica forem diferentes daqueles usados para produzir o relatório armazenado em cache), o servidor de relatório executará novamente o relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Definir opções de processamento &#40;Reporting Services no modo integrado do SharePoint&#41;](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Definir as propriedades do processamento de relatórios](set-report-processing-properties.md)   
 [Conceitos do Reporting Services &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md)   
 [Pré-carregar o cache &#40;Report Manager&#41;](preload-the-cache-report-manager.md)   
 [Agendas](../subscriptions/schedules.md)   
 [Conjuntos de &#40;de armazenamento compartilhados do cache&#41;SSRS](cache-shared-datasets-ssrs.md)   
 [Opções de atualização do cache &#40;Report Manager&#41;](../cache-refresh-options-report-manager.md)  
  
  
