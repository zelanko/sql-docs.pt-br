---
title: Configurar o DQS para usar dados de referência | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.administration.rdsconfiguration.f1
- sql13.dqs.administration.configuration.createDirectRDS.f1
- sql13.dqs.admin.config.rds.f1
ms.assetid: fae745e7-57a7-4cbc-8979-56ea8e392e4e
author: lrtoyou1223
ms.author: lle
manager: jroth
ms.openlocfilehash: ad70828c8b25a9329d5069db204de360900dcb0f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802153"
---
# <a name="configure-dqs-to-use-reference-data"></a>Configurar DQS para usar dados de referência

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve como configurar o [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) para usar dados de referência para limpar seus dados. Você pode usar dados de referência do Windows Azure Marketplace ou de provedores de dados de referência terceirizados online diretos.  

> [!IMPORTANT]
> Este artigo menciona serviços de dados de referência de terceiros que estavam anteriormente disponíveis do Azure DataMarket. DataMarket e Serviços de Dados – incluindo dados de endereço de Melissa, por exemplo – foram descontinuados em 31/12/2016. Como resultado, você não pode executar os exemplos neste artigo com os serviços especificados por meio do DataMarket. Você ainda pode usar os serviços de dados de referência que estão disponíveis online diretamente de provedores de dados de referência de terceiros.

## <a name="before-you-begin"></a>Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para usar dados de referência do Marketplace, você deve ter uma chave de conta válida no Marketplace. Para obter informações detalhadas sobre como criar uma chave de conta do Marketplace, consulte [Criar sua conta](https://go.microsoft.com/fwlink/?LinkId=212936) (https://go.microsoft.com/fwlink/?LinkId=212936). Você também pode criar uma chave de conta do Marketplace no [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] clicando em **Configuração** sob **Administração** na tela de início do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] e depois clicando em **Criar uma ID de Conta do DataMarket** na guia **Dados de Referência** .  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_administrator no banco de dados DQS_MAIN para definir configurações de serviço de dados de referência no DQS.  
  
##  <a name="Marketplace"></a> Configurar o DQS para usar dados de referência do Marketplace  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela de início do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , sob **Administração**, clique em **Configuração**.  
  
3.  Na guia **Dados de Referência** , sob a área **Configurações de Rede** , digite os valores apropriados nas caixas **Servidor Proxy** e **Porta** se você ou sua organização usar o servidor proxy para conectar à Internet.  
  
4.  Especifique a chave de conta do Marketplace na caixa **ID da Contas do DataMarket** e clique no ícone **Validar ID da Conta do DataMarket** para validar a chave de conta. Será exibida uma mensagem para mostrar se a chave de conta do Marketplace é válida.  
  
 Agora você está pronto para usar os serviços de dados de referência do Marketplace no DQS assinados para a chave de conta do Marketplace especificada.  
  
##  <a name="ThirdParty"></a> Configurar o DQS para usar dados de referência de provedores de dados de referência terceirizados online diretos  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela de início do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , sob **Administração**, clique em **Configuração**.  
  
3.  Na guia **Dados de Referência** , sob a área **Configurações de Rede** , digite os valores apropriados nas caixas **Servidor Proxy** e **Porta** se você ou sua organização usar o servidor proxy para conectar à Internet.  
  
4.  Na área **Configurações do Serviço de Dados de Referência Terceirizado Online Direto** , clique no ícone **Adicionar novo provedor de serviço de dados de referência** .  
  
5.  Na caixa de diálogo **Criar Novo Provedor de Serviço de Dados de Referência Terceirizado Online Direto** , especifique os seguintes detalhes:  
  
    1.  Na caixa **Nome** , digite um nome para o novo provedor de serviço de dados de referência direto.  
  
    2.  (Opcional) Na caixa **Descrição** , digite uma descrição para o novo provedor de serviço de dados de referência direto.  
  
    3.  Na caixa **Categoria** , digite a categoria dos dados fornecidos pelo novo provedor de serviço de dados de referência direto.  
  
    4.  Na caixa Esquema, especifique o esquema que define a cadeia de caracteres de campos (nomes de coluna) a ser usada do provedor de serviço de dados de referência direto. Um nome de campo não deve conter um espaço e os campos devem ser separados por vírgulas. Por exemplo: `FirstName, LastName, City, State`.  
  
    5.  Na caixa **URI** , digite a URI do provedor de serviço de dados de referência direto. Apenas URIs seguros (endereço que inicia com "https://") são permitidos no DQS.  
  
    6.  Na caixa **Tamanho Máximo do Lote** , digite o número máximo de registros por lote que serão enviados ao provedor de serviço de dados de referência para limpeza. Um máximo de 100 registros por lote pode ser especificado para a atividade de limpeza.  
  
    7.  Na caixa **ID da Conta** , digite a identificação da conta do assinante no provedor de serviço de dados de referência.  
  
6.  Clique em **OK** para salvar os dados e feche a caixa de diálogo **Criar Novo Provedor de Serviço de Dados de Referência Terceirizado Online Direto** . O provedor de dados de referência terceirizado online direto recém-adicionado ficará disponível na **Grade de Provedores de Serviço de Dados de Referência Diretos** no DQS.  
  
 Agora você está pronto para usar os serviços de dados de referência do provedor de serviço de dados de referência terceirizado online direto recém-configurado no DQS.  
  
##  <a name="FollowUp"></a> Acompanhamento: após configurar o DQS para usar dados de referência  
 Agora você deve mapear os domínios da base de conhecimento necessários para os dados de referência disponíveis nos provedores de dados que acabou de configurar. Para fazer isso, consulte [Anexar um domínio ou um domínio de composição aos dados de referência](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
  
