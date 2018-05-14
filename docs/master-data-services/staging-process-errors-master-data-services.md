---
title: Erros de processo de preparo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], error messages
ms.assetid: 0d9be0dd-638f-4dd4-92b2-253fda655455
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 06d9a8419e908567cfc270dd2ee4a79fbaa42477
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="staging-process-errors-master-data-services"></a>Erros de processo de preparo (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Quando o processo de preparo é concluído, todos os registros processados nas tabelas de preparo têm um valor na coluna ErrorCode. Esses valores são listados na tabela a seguir.  
  
|Código|Erro|Quando ocorre/detalhes|Aplica-se à tabela|  
|----------|-----------|--------------------------|----------------------|  
|210001|O mesmo código de membro existe várias vezes na tabela de preparo.|Seu lote de preparo inclui o mesmo código de membro várias vezes. Nenhum membro é criado ou atualizado.|Folha<br /><br /> Consolidado<br /><br /> Relação|  
|210003|Os valores de atributos fazem referência a um membro que não existe ou está inativo.|Quando você prepara atributos baseados em domínio, deve usar o código, em lugar do nome. Aplica-se a **ImportType0**, **1**e **2**.|Folha<br /><br /> Consolidado|  
|210006|O código de membro está inativo.|**ImportType** = **1** e você especificou um código de membro que não existe.|Folha<br /><br /> Consolidado<br /><br /> Relação|  
|210032|O nome da hierarquia está ausente ou não é válido.|A hierarquia explícita não foi encontrada ou o valor de **HierarchyName** estava em branco.|Consolidado<br /><br /> Relação|  
|210035|Como não existe uma regra de negócio de geração de código, o **MemberCode** é necessário.|Ao criar ou atualizar membros, um **MemberCode** sempre é necessário, a menos que você esteja usando a geração de código automática. Para obter mais informações, consulte [Criação automática de código &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md).|Folha<br /><br /> Consolidado|  
|210036|Como existe uma regra de negócio de geração de código, o **MemberCode** não é necessário.|Ao criar ou atualizar membros, um **MemberCode** não é necessário quando você está usando a geração de código automática. Porém, se preferir, você poderá especificar um código. Para obter mais informações, consulte [Criação automática de código &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md).|Folha<br /><br /> Consolidado|  
|210041|"ROOT" não é um código de membro válido.|O valor de **MemberCode** contém a palavra “ROOT”.|Folha<br /><br /> Consolidado<br /><br /> Relação|  
|210042|"MDMUNUSED" não é um código de membro válido.|O valor de **MemberCode** contém a palavra “MDMUNUSED”.|Folha<br /><br /> Consolidado<br /><br /> Relação|  
|210052|O MemberCode não pode ser desativado porque é usado como um valor de atributo baseado em domínio.|Quando **ImportType** = **3** ou **4**, o preparo falhará se o membro for usado como um valor de atributo para outros membros. Use **ImportType5** ou **6** para definir o valor como NULL ou altere os valores antes de executar o processo de preparo.|Folha<br /><br /> Consolidado|  
|300002|O código de membro não é válido.|Relações: o código de membro pai ou filho não existe.<br /><br /> Folha ou Consolidado: **ImportType** = **3** ou **4** e o código de membro não existe.|Folha<br /><br /> Consolidado<br /><br /> Relação|  
|300004|O código de membro já existe.|**ImportType** = **1** e você usou um código de membro que já existe na entidade.|Folha<br /><br /> Consolidado|  
|210011|Quando **RelationshipType** é **1**, o **ParentCode** não pode ser um membro folha.|Verifique se o valor de **ParentCode** é um código de membro consolidado.|Relação|  
|210015|O código de membro existe várias vezes na tabela de preparo para uma hierarquia e um lote.|Para uma hierarquia explícita, você especificou o local do mesmo membro várias vezes no mesmo lote.|Relação|  
|210016|Não foi possível criar a relação porque ela causaria uma referência circular.|Isso ocorre quando você tenta atribuir um filho como um pai.|Relação|  
|210046|O membro não pode ser um irmão de Root.|Isso ocorre quando **RelationshipType** = **2** (irmão) e o **ParentCode** ou **ChildCode** é **Root**. Membros não podem estar no mesmo nível do nó raiz; eles só podem ser filhos.|Relação|  
|210047|O membro não pode ser um irmão de Unused.|Isso ocorre quando **RelationshipType** = **2** (irmão) e o **ParentCode** ou **ChildCode** é **Unused**. Os membros podem ser filhos apenas do nó Unused.|Relação|  
|210048|**ParentCode** e **ChildCode** não podem ser iguais.|O valor de **ParentCode** é igual ao valor de **ChildCode** . Esses valores devem ser diferentes.|Relação|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir erros que ocorrem durante o preparo &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
  
