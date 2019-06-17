---
title: Alterar o tipo de atributo (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9d3001d9-8d0f-4e4a-8e04-4f666bf0df69
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4406eb225002bbf5df93f8c67385694922d7d2c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482760"
---
# <a name="change-the-attribute-type-mds-add-in-for-excel"></a>Alterar o tipo de atributo (suplemento MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], os administradores podem alterar o tipo de atributo quando o tipo de dados ou número de caracteres permitido está incorreto.  
  
 Se você quiser alterar o tipo de atributo para criar uma lista restrita (atributo baseado em domínio), consulte [Criar um atributo baseado em domínio &#40;Suplemento MDS para Excel&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md).  
  
> [!NOTE]  
>  Não é possível atualizar o tipo ou o tamanho da coluna **Nome** ou **Código**.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você precisa ter permissão para acessar as áreas funcionais **Administração do Sistema** e **Gerenciador** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../administrators-master-data-services.md).  
  
-   Deve haver um modelo, entidade e atributo existente.  
  
### <a name="to-change-the-attribute-type"></a>Para alterar o tipo de atributo  
  
1.  No Excel, carregue a entidade que contém a coluna (atributo) a ser alterada. Para obter mais informações, consulte [carregar dados do MDS no Excel](export-data-to-excel-from-master-data-services.md).  
  
2.  Clique em qualquer célula da coluna que você deseja alterar.  
  
3.  No grupo **Compilar Modelo** , clique em **Propriedades do Atributo**.  
  
4.  Na caixa de diálogo **Propriedades do Atributo** , é necessário atualizar as configurações.  
  
5.  Clique em **OK**.  
  
## <a name="what-happens-when-you-change-the-attribute-type"></a>O que acontece quando você altera o tipo de atributo?  
 Se houver qualquer dependência no atributo, por exemplo, o atributo ser referenciado por qualquer regra de negócio do MDS ou o atributo ser incluído em uma exibição de assinatura, e você alterar o tipo de dados de um atributo, o MD irá:  
  
-   Alterar o tipo de dados do atributo.  
  
-   Gere uma cópia do atributo com o sufixo old"que não contém qualquer valor. Isso é chamado de um **preterido** atributo.  
  
 Porém, todas as dependências existentes no atributo original apontarão para o atributo substituído, e não para o alterado.  
  
 Isso significa que:  
  
-   Você deve atualizar as regras de negócio para apontar para o atributo alterado porque a lógica pode não ser a mesma considerando o novo tipo de dados do atributo. Será necessário editar cada regra afetada e, em seguida, retrabalhar as expressões para apontar para remover as referências do atributo substituído (_old) para apontar para o atributo atualizado.  
  
-   Você deve abrir todas as exibições de assinatura na seleção de gerenciamento de integração, selecione a linha da exibição, abri-lo para edição clicando no ícone de lápis e, em seguida, clique no **salvar disco** ícone para atualizar a definição da exibição. Nenhuma outra alteração é necessária para regenerar a sintaxe da exibição.  
  
-   As tabelas de preparo que incluem o atributo terão uma coluna de atributo substituído adicionada a ele, o que significa que o código de preparação será afetado. Para livrar-se do atributo substituído, você poderá excluí-lo depois de atualizar as regras de negócio e as exibições de assinatura.  
  
 **Excluindo o atributo substituído**  
  
 Antes de excluir qualquer atributo substituído, você deverá remover as referências ao atributo, por exemplo, corrigindo as regras de negócio e regenerando as exibições de assinatura conforme descrito anteriormente. Caso contrário, você obterá um erro na página da Web da administração do sistema ao tentar excluir o atributo substituído indicando que o atributo não poderá ser excluído porque é referenciado por um objeto.  
  
 Para excluir um atributo, consulte [excluir um atributo &#40;Master Data Services&#41;](../delete-an-attribute-master-data-services.md)  
  
> [!TIP]  
>  É incômodo alterar tipos de dados para os atributos do MDS que tenham dados existentes e entidades relacionadas, especialmente se houver uma regra de negócio ou uma exibição de assinatura declarada que depende da entidade. A prática recomendada é iniciar com um tipo de dados que é flexível o suficiente para manter os valores necessários. Por exemplo, as cadeias de caracteres podem começar pequenas, mas podem precisar ser aumentadas com o passar do tempo; portanto, considere o pior cenário. O comprimento adicional de cadeia de caracteres de texto pode ser penoso (por exemplo, é difícil ajustar na tela as caixas de texto largas da GUI), portanto evite o comprimento muito longo da cadeia de caracteres.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos &#40;Master Data Services&#41;](../attributes-master-data-services.md)   
 [Criando um modelo &#40;Suplemento MDS para Excel&#41;](building-a-model-mds-add-in-for-excel.md)  
  
  
