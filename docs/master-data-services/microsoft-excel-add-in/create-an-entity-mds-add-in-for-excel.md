---
title: Criar uma entidade (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: microsoft-excel-add-in
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d354abb3-88fe-4b40-a374-f6256b84ffae
caps.latest.revision: 8
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: c60ebbff3b77ce4b45eacf082f9f5e427741ff5d
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="create-an-entity-mds-add-in-for-excel"></a>Criar uma entidade (Suplemento do MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], os administradores podem criar novas entidades para armazenar dados. Quando você cria uma entidade, deve carregar pelo menos uma amostragem dos dados que deseja armazenar.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você precisa ter permissão para acessar as áreas funcionais **Administração do Sistema** e **Gerenciador** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md).  
  
-   Você deve ter um modelo existente no qual criar a entidade. Para obter mais informações, consulte [Criar um modelo &#40;Master Data Services&#41;](../../master-data-services/create-a-model-master-data-services.md).  
  
-   Verifique se seus dados atendem aos requisitos seguintes:  
  
    -   Os dados devem ter uma linha de cabeçalho.  
  
    -   É útil ter colunas **Nome** e **Código** . **Código** é um identificador exclusivo de cada linha.  
  
    -   Você deve ter pelo menos uma linha de dados diferente do cabeçalho. Nem todas as colunas precisam de valores, mas os dados devem ser representativos dos dados que estarão na entidade.  
  
    -   Se houver uma coluna que contém um identificador exclusivo (conhecido no MDS como **Código**), verifique se os valores são exclusivos. Se nenhuma coluna contiver identificadores, você poderá tê-los gerado automaticamente ao criar a entidade.  
  
    -   Verifique se nenhuma célula contém fórmulas.  
  
    -   Verifique se nenhuma célula valores de hora. Valores de data podem ser salvos no MDS, mas valores de hora não podem.  
  
### <a name="to-create-an-entity-and-load-data"></a>Para criar uma entidade e carregar dados  
  
1.  Abra ou crie uma planilha do Excel que contenha os dados que você deseja carregar.  
  
2.  Selecione as células que você deseja carregar na nova entidade.  
  
3.  Na guia **Dados Mestre** , no grupo **Compilar Modelo** , clique em **Criar Entidade**.  
  
4.  Se você for solicitado a se conectar a um repositório do MDS, faça isso.  
  
5.  Na caixa de diálogo **Criar Entidade** , deixe o intervalo padrão ou altere-o para aplicar aos dados que você deseja carregar.  
  
6.  Não desmarque a caixa de seleção **Meus dados têm cabeçalhos** .  
  
7.  Na lista **Modelo** , selecione um modelo.  
  
8.  Na lista **Versão** , selecione uma versão.  
  
9. Na caixa **Nome da nova entidade** , digite um nome para a entidade.  
  
10. Na lista **Código** , selecione a coluna que contém identificadores exclusivos ou que tem códigos gerados automaticamente.  
  
11. Opcional. Na lista **Nome** , selecione uma coluna que contém nomes para cada membro.  
  
12. Clique em **OK**. Após a criação com êxito da entidade, uma nova linha de cabeçalho é exibida, as células são realçadas e o nome da planilha é atualizado para corresponder ao nome da entidade.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Para exibir os erros que ocorreram, no grupo **Publicar e Validar** , clique em **Mostrar Status**. As colunas ValidationStatus e InputStatus são exibidas. Para obter mais informações, consulte [Validando dados &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md).  
  
-   Confirme se os atributos foram criados como o tipo de dados esperado.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um atributo baseado em domínio &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)  
  
  

