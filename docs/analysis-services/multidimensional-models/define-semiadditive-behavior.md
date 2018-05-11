---
title: Definir comportamento Semiaditivo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6be002e501e7cc77dcd3ad312c8560698d4c116f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="define-semiadditive-behavior"></a>Definir um comportamento semiaditivo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Medidas semiaditivas, que não agregam uniformemente todas as dimensões, são muito comuns em muitos cenários empresariais. Todo cubo que se baseia em instantâneos de balanços, com o decorrer do tempo, apresenta esse problema. Você encontra esses instantâneos em aplicativos que cuidam de títulos, saldos de contas, orçamentos, recursos humanos, apólices de seguros e sinistros e em vários outros domínios empresariais.  
  
 Adicione um comportamento semiaditivo a um cubo para definir um método de agregação para medidas ou membros individuais de um atributo de tipo de conta. Se o cubo contiver uma dimensão de conta, é possível definir automaticamente o comportamento semiaditivo de acordo com o tipo de conta.  
  
 Para adicionar um comportamento semiaditivo, abra um cubo no Designer de Cubo e escolha **Adicionar Business Intelligence** no menu Cubo. No Assistente de Business Intelligence, selecione a opção **Definir comportamento semiaditivo** na página **Escolher Aprimoramento** . Esse assistente orienta você pelas etapas para identificar quais medidas têm comportamento semiaditivo.  
  
 Com exceção de LastChild que está disponível na edição standard, os comportamentos semiaditivos só estão disponíveis nas edições business intelligence ou enterprise.  
  
## <a name="define-semiadditive-behavior"></a>Definir um comportamento semiaditivo  
 Na página **Definir Comportamento Semiaditivo** do assistente, selecione como definir o aspecto semiaditivo selecionando uma destas opções:  
  
 **Desativar comportamento semiaditivo**  
 Remove o comportamento semiaditivo de um cubo no qual ele foi previamente definido. Essa seleção redefinirá uma medida como **SUM** se ela estiver configurada como algum destes tipos de função de agregação:  
  
-   Por Conta  
  
-   Average of Children  
  
-   First Child  
  
-   Último Filho  
  
-   Último Filho Não Vazio  
  
-   Primeiro Filho Não Vazio  
  
-   Nenhuma  
  
 Essa opção não altera as medidas com uma função de agregação regular: **Sum**, **Min**, **Max**, **Count**ou **Distinct****Count**.  
  
 **O assistente detectou a dimensão de conta 'Conta", que contém membros semiaditivos. O servidor agregará membros dessa dimensão de acordo com o comportamento semiaditivo especificado para cada tipo de conta.**  
 Faz com que o sistema configure todas as medidas de um grupo de medidas de uma dimensão por uma dimensão do tipo Conta para a função de agregação Por Conta e o servidor agregará os membros da dimensão de acordo com o comportamento semiaditivo especificado para cada tipo de conta.  
  
> [!NOTE]  
>  Essa opção será selecionada por padrão se o assistente detectar uma dimensão de tipo Conta.  
  
 **Definir comportamento semiaditivo para medidas individuais**  
 Seleciona o comportamento semiaditivo de cada medida individualmente. A configuração padrão é **SUM** (completamente aditivo).  
  
> [!NOTE]  
>  Essa opção será selecionada por padrão se o assistente não detectar uma dimensão de tipo Conta.  
  
 Para cada medida, você pode selecionar um dos tipos de funcionalidade semiaditiva descritos na tabela a seguir.  
  
|Função semiaditiva|Description|  
|---------------------------|-----------------|  
|Average of Children|A agregação de um membro é a média de seus filhos.|  
|ByAccount|O sistema lê o comportamento de semiaditivo especificado para o tipo de conta.|  
|Count|A agregação é uma contagem de membros.|  
|Contagem Distinta|A agregação é uma contagem de membros exclusivos.|  
|First Child|O valor do membro é avaliado como o valor de seu primeiro filho juntamente com a dimensão de tempo.|  
|FirstNonEmpty|O valor do membro é avaliado como o valor de seu primeiro filho juntamente com a dimensão que contém dados.|  
|LastChild|O valor do membro é avaliado como o valor de seu último filho juntamente com a dimensão de tempo.|  
|LastNonEmpty|O valor do membro é avaliado como o valor de seu último filho juntamente com a dimensão que contém dados.|  
|Max|A função de agregação máxima é aplicada.|  
|Min|A função de agregação mínima é aplicada.|  
|Nenhum.|Nenhuma agregação é aplicada.|  
|SUM|A função de soma padrão é aplicada.|  
  
 Qualquer comportamento semiaditivo existente será substituído quando você concluir o assistente.  
  
  
