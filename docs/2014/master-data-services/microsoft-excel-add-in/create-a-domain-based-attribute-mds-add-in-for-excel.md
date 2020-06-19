---
title: Criar um atributo baseado em domínio (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 7b3e30dc-8f41-4a5d-8009-ae5a4426a64b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 93a22979296e397ebe9c28a014913ca9da592ee6
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84961316"
---
# <a name="create-a-domain-based-attribute-mds-add-in-for-excel"></a>Criar um atributo baseado em domínio (Suplemento do MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], os administradores podem criar um atributo baseado em domínio quando desejarem restringir os valores em uma coluna a um conjunto específico de valores.  
  
 Os valores já podem estar na planilha ou podem vir de uma entidade existente.  
  
> [!NOTE]  
>   Se os usuários digitarem um valor na coluna restrita, em vez de selecionar na lista, serão exibidos erros na coluna **$ InputStatus $** quando eles publicarem.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você precisa ter permissão para acessar as áreas funcionais **Administração do Sistema** e **Gerenciador** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../administrators-master-data-services.md).  
  
-   O modelo e a entidade já devem existir.  
  
### <a name="to-perform-this-procedure"></a>Para executar esse procedimento:  
  
1.  No Excel, carregue a entidade que contém a coluna (atributo) a ser restringida. Para obter mais informações, consulte [carregar dados do MDS para o Excel](export-data-to-excel-from-master-data-services.md).  
  
2.  Clique em qualquer célula da coluna que você deseja restringir.  
  
3.  No grupo **Compilar Modelo** , clique em **Propriedades do Atributo**.  
  
4.  Na caixa de diálogo **Propriedades de Atributo** , na lista **Tipo de atributo** , escolha **Lista restrita (baseada em domínio)**.  
  
5.  Na lista **Popular o atributo com valores de** :  
  
    -   Para usar valores da planilha, escolha **a coluna selecionada**. Serão criadas uma nova entidade e uma nova tabela de preparo com os valores da coluna selecionada.  
  
    -   Para usar valores de uma entidade existente, escolha o nome da entidade.  
  
6.  Se você escolheu **a coluna selecionada** na etapa anterior, na caixa **Novo nome da entidade** , digite um nome para a nova entidade. Esse pode ser igual ao nome da coluna (atributo).  
  
7.  Clique em **OK**. Agora, cada célula na coluna tem uma lista de valores que os usuários podem escolher.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Para adicionar e excluir valores na lista restrita, carregue a entidade na qual o atributo se baseia. Para obter mais informações sobre como carregar entidades, consulte [carregar dados do MDS para o Excel](export-data-to-excel-from-master-data-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Atributos baseados em domínio &#40;Master Data Services&#41;](../domain-based-attributes-master-data-services.md)   
 [Criar uma entidade &#40;Suplemento MDS para Excel&#41;](create-an-entity-mds-add-in-for-excel.md)   
 [Criando um modelo &#40;Suplemento MDS para Excel&#41;](building-a-model-mds-add-in-for-excel.md)  
  
  
