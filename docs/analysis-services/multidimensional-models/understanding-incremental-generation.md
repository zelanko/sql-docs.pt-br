---
title: Noções básicas sobre geração Incremental | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 71b3f839326bec0a8b5606e2c7de3f25584b4ff1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024343"
---
# <a name="understanding-incremental-generation"></a>Entendendo a geração com incremento
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Após a geração de esquema inicial, você pode alterar as definições do cubo e das dimensões usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e, em seguida, executar novamente o Assistente de Geração de Esquema. O assistente atualiza o esquema do banco de dados da área de assunto e da exibição da fonte de dados associada para refletir as mudanças, mantendo, na medida do possível, os dados que já existem nas tabelas que serão geradas novamente. Se você alterou as tabelas depois da geração inicial, o Assistente de Geração de Esquema preservará essas alterações sempre que possível usando as seguintes regras:  
  
-   Se uma tabela foi previamente gerada pelo assistente, ela será substituída. Você pode evitar que a tabela gerada pelo assistente seja substituída alterando a propriedade **AllowChangesDuringGeneration** da tabela da exibição da fonte de dados para **false**. Quando você assume o controle de uma tabela, ela passa a ser tratada como qualquer outra tabela definida pelo usuário e não é afetada durante a nova geração. Depois de remover uma tabela da nova geração, você pode alterar a propriedade **AllowChangesDuringGeneration** da tabela da exibição da fonte de dados para **true** e reabri-la para fazer as alterações do assistente. Para obter mais informações, consulte [Alterar propriedades em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md).  
  
-   Se a tabela foi adicionada à exibição da fonte de dados ou ao banco de dados subjacente de outra forma que não pelo assistente, ela não será substituída.  
  
 Quando o Assistente de Geração de Esquema gerar novamente as tabelas que antes eram geradas no banco de dados da área de assunto, pode ser preferível que o assistente preserve os dados existentes nessas tabelas.  
  
## <a name="supporting-data-preservation"></a>Oferecendo suporte a preservação dos dados  
 Como regra geral, o Assistente de Geração de Esquema preserva os dados que estão armazenados nas tabelas por ele geradas. Além disso, se você adicionar colunas a tabelas que o assistente gerou, este preservará também os dados. Você pode usar esse recurso para adicionar ou modificar dimensões e cubos e, em seguida, gerar novamente os objetos subjacentes sem precisar recarregar os dados armazenados nas tabelas subjacentes.  
  
> [!NOTE]  
>  Se você estiver carregando dados de arquivos de texto delimitados, poderá também decidir se o Assistente de Geração de Esquema substituirá esses arquivos e os dados neles contidos durante a nova geração. Os arquivos de texto podem ser totalmente substituídos ou não. O Assistente de Geração de Esquema não substitui os arquivos parcialmente. Por padrão, esses arquivos não são substituídos.  
  
### <a name="partial-preservation"></a>Preservação parcial  
 O Assistente de Geração de Esquema não pode preservar os dados existentes em algumas situações. A tabela a seguir fornece exemplos de situações em que o assistente não é capaz de preservar todos os dados existentes nas tabelas subjacentes durante a nova geração.  
  
|Alteração do tipo de dados|Tratamento|  
|-------------------------|---------------|  
|Alteração de tipo de dados incompatível|Sempre que possível, o Assistente de Geração de Esquema utiliza conversões do tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] padrão para converter os dados existentes de um tipo de dados para outro. No entanto, quando você altera o tipo de dados de um atributo para um tipo incompatível com os dados existentes, o assistente descarta os dados da coluna afetada.|  
|Erros de integridade referencial|Se você alterar uma dimensão ou um cubo que contém dados e a alteração causar um erro de integridade referencial durante a nova geração, o Assistente de Geração de Esquema descartará todos os dados da tabela de chave estrangeira. Os dados que são descartados não se limitam à coluna que causou a violação de restrição da chave estrangeira nem às linhas que contêm os erros de integridade referencial. Por exemplo, se você alterar a chave da dimensão para um atributo que possui dados nulos ou não exclusivos, todos os dados existentes na tabela de chave estrangeira serão descartados. Além disso, o descarte de todos os dados de uma tabela pode ter um efeito dominó e causar outras violações de integridade referencial.|  
|Atributo ou dimensão excluído(a)|Se você excluir um atributo de uma dimensão, o Assistente de Geração de Esquema excluirá a coluna que está mapeada para o atributo excluído. Se você excluir uma dimensão, o assistente excluirá a tabela mapeada para a dimensão excluída. Nesses casos, o assistente descartará os dados contidos na coluna ou tabela excluída.|  
  
 O Assistente de Geração de Esquema emite um aviso antes de descartar os dados, de modo que é possível cancelar o assistente sem perder dados. No entanto, o Assistente de Geração de Esquema não consegue diferenciar entre a perda de dados prevista e a perda de dados imprevista. Quando você executa o assistente, uma caixa de diálogo lista as tabelas e colunas que contêm dados que serão descartados. Você pode deixar o assistente prosseguir e descartar os dados ou cancelá-lo e revisar as alterações feitas nas tabelas e colunas.  
  
## <a name="supporting-cube-and-dimension-changes"></a>Suporte para alterações em cubos e dimensões  
 Quando você altera as propriedades de dimensões e cubos, o Assistente de Geração de Esquema gera novamente os objetos apropriados no banco de dados da área de assunto subjacente, bem como da exibição da fonte de dados relacionada, conforme descrito na tabela a seguir.  
  
 Excluindo um objeto, como uma dimensão, cubo ou atributo.  
 O Assistente de Geração de Esquema exclui os objetos subjacentes para os quais o objeto excluído está mapeado. Se você adicionar colunas a uma tabela que o assistente gerou, as novas colunas não impedirão a exclusão da tabela. A exclusão de um objeto faz com que os dados armazenados nos objetos subjacentes sejam descartados e também pode fazer com outros dados sejam descartados se ocorrerem erros de integridade referencial.  
  
 Renomeando um objeto, como uma dimensão, cubo ou atributo.  
 O Assistente de Geração de Esquema renomeia os objetos subjacentes para os quais o objeto renomeado está mapeado. O assistente também renomeia todos os objetos afetados, como as chaves primárias. Os dados existentes armazenados nos objetos subjacentes são preservados.  
  
 Modificando um objeto, como a alteração de seu tipo de dados.  
 O Assistente de Geração de Esquema modifica os objetos subjacentes para os quais o objeto modificado está mapeado. Os dados existentes armazenados nos objetos subjacentes dos bancos de dados são preservados, exceto se o novo tipo de dados for incompatível com os dados existentes.  
  
 Adicionando um novo objeto, como uma dimensão, cubo ou atributo.  
 O Assistente de Geração de Esquema adiciona objetos subjacentes para os quais o novo objeto está mapeado.  
  
 Se o Assistente de Geração de Esquema não puder fazer a alteração necessária porque existe um objeto de usuário no banco de dados da área de assunto (porque o Database Engine retorna um erro), ocorrerá uma falha do Assistente de Geração de Esquema e ele exibirá o erro retornado pelo Database Engine. Por exemplo, se você criar uma restrição de chave primária ou um índice não clusterizado de uma tabela depois que o assistente gerar novamente a tabela, o Assistente de Geração de Esquema não descartará essa tabela porque ele não criou a restrição nem o índice.  
  
## <a name="supporting-schema-changes"></a>Suporte a alterações de esquema  
 Quando você alterar as propriedades de tabelas ou colunas do banco de dados da área de assunto ou da exibição da fonte de dados associada, o Assistente de Geração de Esquema tratará as alterações conforme descrito na tabela a seguir.  
  
 Exclusão de uma tabela ou uma coluna gerada pelo Assistente de Geração de Esquema.  
 Se você excluir uma tabela ou coluna gerada pelo Assistente de Geração de Esquema, o assistente gerará novamente tabela excluída. O assistente não fornece nenhum aviso de que a tabela ou coluna excluída será gerada novamente.  
  
 Alteração das propriedades de uma tabela ou coluna gerada pelo Assistente de Geração de Esquema.  
 Se você modificar as propriedades de uma tabela ou coluna gerada pelo Assistente de Geração de Esquema, o assistente gerará a tabela alterada sem a alteração. Por exemplo, se você alterar o tipo de dados, a nulidade de uma coluna ou o grupo de arquivos de uma tabela gerada pelo Assistente de Geração de Esquema, a alteração não será preservada após a nova geração. O assistente não fornece nenhum aviso de que o objeto alterado será gerado novamente sem a alteração.  
  
 Adição de uma coluna a uma tabela gerada pelo Assistente de Geração de Esquema ou de uma tabela ao banco de dados da área de assunto ou ao banco de dados da área de preparação.  
 Se você adicionar uma coluna a uma tabela gerada pelo Assistente de Geração de Esquema, o assistente preservará a coluna adicional além de todos os dados armazenados nela durante a nova geração. No entanto, se você adicionar uma tabela gerada ao banco de dados da área de assunto ou ao banco de dados da área de preparação, o Assistente de Geração de Esquema não incorporará a nova tabela. A coluna, ou tabela, adicionada não aparecerá no projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , nos pacotes DTS, na exibição da fonte de dados ou em nenhum outro ponto do esquema que é gerado.  
  
## <a name="supporting-data-source-and-data-source-view-changes"></a>Suporte a alterações em fontes de dados e em exibições da fonte de dados  
 Quando o Assistente de Geração de Esquema é executado novamente, ele reutiliza a fonte de dados e a exibição da fonte de dados usadas na geração original. Se você adicionar uma fonte de dados ou uma exibição da fonte de dados, o assistente não a usará. Se você excluir a fonte de dados ou a exibição da fonte de dados original depois da geração inicial, execute o assistente desde o início. Também são excluídas todas as configurações anteriores do assistente. Todos os objetos existentes em um banco de dados subjacente que estavam vinculados a uma fonte de dados ou exibição de fonte de dados excluída serão tratados como objetos criados pelo usuário na próxima vez que você executar o Assistente de Geração de Esquema.  
  
 Se a exibição da fonte de dados não refletir o estado real do banco de dados subjacente no momento da geração, o Assistente de Geração de Esquema pode encontrar erros ao gerar esquemas para o banco de dados da área de assunto ou da área de preparação. Por exemplo, se a exibição da fonte de dados especificar que o tipo de dados de uma coluna deve ser configurado como **int**, mas, na verdade, o tipo de dados da coluna estiver configurado como **string**, o Assistente de Geração de Esquema definirá o tipo de dados da chave estrangeira como **int** de acordo com a exibição da fonte de dados e, em seguida, não conseguirá criar a relação pois o tipo de dados real é **string**.  
  
 Por outro lado, se você alterar a cadeia de conexão da fonte de dados para um banco de dados diferente daquele usado na geração anterior, nenhum erro será gerado. O novo banco de dados será usado e nenhuma alteração será feita no banco de dados anterior.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar alterações em exibições da fonte de dados e fontes de dados](../../analysis-services/multidimensional-models/manage-changes-to-data-source-views-and-data-sources.md)   
 [Assistente de geração de esquema & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/schema-generation-wizard-analysis-services.md)  
  
  
