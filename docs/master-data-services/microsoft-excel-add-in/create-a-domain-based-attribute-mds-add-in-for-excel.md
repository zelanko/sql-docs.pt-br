---
title: "Criar um atributo baseado em domínio (Suplemento MDS para Excel) | Microsoft Docs"
ms.custom: 
ms.date: 07/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b3e30dc-8f41-4a5d-8009-ae5a4426a64b
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 0183ba6f178fbc9f392b4e711ccaba49220ffa3e
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="create-a-domain-based-attribute-mds-add-in-for-excel"></a>Criar um atributo baseado em domínio (Suplemento do MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], os administradores podem criar um atributo baseado em domínio quando desejarem restringir os valores em uma coluna a um conjunto específico de valores.  
  
 Os valores já podem estar na planilha ou podem vir de uma entidade existente.  
  
> [!NOTE]  
>  Se os usuários digitarem um valor na coluna restrita, em vez de selecionar na lista, serão exibidos erros na coluna **$InputStatus$** quando eles publicarem.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você precisa ter permissão para acessar as áreas funcionais **Administração do Sistema** e **Gerenciador** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md).  
  
-   O modelo e a entidade já devem existir.  
  
### <a name="to-perform-this-procedure"></a>Para executar esse procedimento:  
  
1.  No Excel, carregue a entidade que contém a coluna (atributo) a ser restringida. Para obter mais informações, consulte [Exportar dados para o Excel do Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md).  
  
2.  Clique em qualquer célula da coluna que você deseja restringir.  
  
3.  No grupo **Compilar Modelo** , clique em **Propriedades do Atributo**.  
  
4.  Na caixa de diálogo **Propriedades de Atributo** , na lista **Tipo de atributo** , escolha **Lista restrita (baseada em domínio)**.  
  
5.  Na lista **Popular o atributo com valores de** :  
  
    -   Para usar valores da planilha, escolha **a coluna selecionada**. Serão criadas uma nova entidade e uma nova tabela de preparo com os valores da coluna selecionada.  
  
    -   Para usar valores de uma entidade existente, escolha o nome da entidade.
    
    Se houver mais de 50 entidades, você poderá filtrar e pesquisar por uma entidade. Caso contrário, selecione uma entidade na lista suspensa.  
  
6.  Se você escolheu **a coluna selecionada** na etapa anterior, na caixa **Novo nome da entidade** , digite um nome para a nova entidade. Esse pode ser igual ao nome da coluna (atributo).  
  
7.  Clique em **OK**. Agora, cada célula na coluna tem uma lista de valores que os usuários podem escolher.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Para adicionar e excluir valores na lista restrita, carregue a entidade na qual o atributo se baseia. Para obter mais informações sobre como carregar entidades, consulte [Exportar dados para o Excel do Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Atributos baseados em domínio &#40;Master Data Services&#41;](../../master-data-services/domain-based-attributes-master-data-services.md)   
 [Criar uma entidade &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)   
 [Criar um modelo &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
  
