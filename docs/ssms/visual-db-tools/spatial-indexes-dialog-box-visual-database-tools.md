---
title: Caixa de diálogo Índices Espaciais (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.spatialindexes
ms.assetid: 4d84239a-68c7-4aa2-8602-2b51dd07260f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a4d8ce987edf5595c0f1f75bb0da6d94c5399033
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263567"
---
# <a name="spatial-indexes-dialog-box-visual-database-tools"></a>Caixa de diálogo Índices Espaciais (Ferramentas de Banco de Dados Visual)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Use a caixa de diálogo **Índices Espaciais** em colunas de tipo de dados de **geometria** ou **geografia** (*colunas espaciais*), que não podem ser indexadas usando a caixa de diálogo **Índice/Chaves** . Cada coluna espacial pode ter mais de um índice espacial, mas eles devem ser criados um de cada vez.  
  
Para obter informações sobre restrições de criação de índices espaciais, consulte [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
## <a name="options"></a>Opções  
**Índice Espacial Selecionado**  
Lista os índices espaciais existentes. Selecione um índice para mostrar suas propriedades. Se a lista estiver vazia, nenhum índice espacial foi definido para a tabela.  
  
**Adicionar**  
Cria um novo índice espacial.  
  
**Delete (excluir)**  
Exclui o índice espacial selecionado na lista **Índice Espacial Selecionado** .  
  
**Células por Objeto**  
Indica o número de células por objeto do mosaico que pode ser usado para um único objeto espacial no índice. Esse número pode ser qualquer inteiro entre 1 e 8.192, inclusive. O padrão é 16.  
  
Se um objeto abranger mais células do que o especificado por *n*, a indexação usará tantas células quantas forem necessárias para fornecer um mosaico de nível superior completo. Nesses casos, um objeto poderia receber mais que o número de células especificado. Nesse caso, o número máximo de células geradas pela grade de nível superior, que depende da densidade **Nível 1** .  
  
**Colunas**  
Indica o nome de coluna e a ordem de classificação.  
  
**IsSpatialIndex**  
Indica que um índice espacial está selecionado.  
  
**Nível 1**  
Indica a densidade da grade de primeiro nível (superior).  
  
**Nível 2**  
Indica a densidade da grade de segundo nível.  
  
**Nível 3**  
Indica a densidade da grade de terceiro nível.  
  
**Nível 4**  
Indica a densidade da grade de quarto nível.  
  
**Esquema de Mosaico**  
Indica o esquema de mosaico do índice:  
  
Opções da coluna**Geometria** :  
  
-   **Grade geométrica** para uma coluna de geometria  
  
-   **Grade geográfica** para uma coluna de geografia  
  
**Tipo**  
Indica que um índice espacial está selecionado.  
  
**X-max**  
Especifica a coordenada x do canto superior direito da caixa delimitadora. Esta propriedade ficará esmaecida se o **Esquema de Mosaico** for **Grade geográfica**.  
  
**X-min**  
Especifica a coordenada x do canto inferior esquerdo da caixa delimitadora. Esta propriedade ficará esmaecida se o **Esquema de Mosaico** for **Grade geográfica**.  
  
**Y-max**  
Especifica a coordenada y do canto superior direito da caixa delimitadora. Esta propriedade ficará esmaecida se o **Esquema de Mosaico** for **Grade geográfica**.  
  
**Y-min**  
Especifica a coordenada y do canto inferior esquerdo da caixa delimitadora. Esta propriedade ficará esmaecida se o **Esquema de Mosaico** for **Grade geográfica**.  
  
**Identidade**  
Quando expandida, mostra os campos de propriedade **Nome** e **Descrição** .  
  
**(Nome)**  
Mostra o nome do índice espacial. Quando um novo índice é criado, é dado um nome padrão baseado na tabela da janela ativa no Designer de Tabela. O nome pode ser alterado a qualquer momento.  
  
**Descrição**  
Descreve o índice. Para escrever uma descrição mais detalhada, clique em **Descrição** e, em seguida, clique no botão de reticências ( **…** ) que aparece à direita do campo de propriedade. Isso criará uma área maior para a redação do texto.  
  
**Categoria do Designer de Tabelas**  
Quando expandida, mostra informações sobre as propriedades desse índice espacial.  
  
**Especificação de preenchimento**  
Quando expandido, mostra informações de **Fator de Preenchimento** e **Preenchimento de índice**.  
  
**Fator de Preenchimento**  
Especifica a porcentagem da página de índice que o sistema poderá preencher. Quando a página estiver preenchida, se novos dados forem adicionados, o sistema precisará dividir a página, o que compromete o desempenho.  
  
-   Um valor de 100 significa que as páginas serão preenchidas; isso exige o espaço mínimo de armazenamento mas é o menos eficaz. Essa configuração só deverá usada quando não houver alterações de dados; por exemplo, em uma tabela somente leitura.  
  
-   Um valor inferior propicia mais espaço vazio nas páginas de dados, o que reduz a necessidade de dividir as páginas de dados à medida que os índices aumentam. Porém, isso requer mais espaço de armazenamento. Essa configuração é mais adequada quando houver alterações nos dados da tabela.  
  
**Preenchimento de índice**  
Fornece páginas nesse índice com o mesmo percentual de espaço vazio (preenchimento) especificado em **Fator de Preenchimento**.  
  
**Bloqueios de página permitidos**  
Especifica se o bloqueio de página é permitido no índice. A permissão ou não dos bloqueios de página afeta o desempenho do banco de dados.  
  
**Recalcular estatísticas**  
Especifica se as novas estatísticas deverão ser recalculadas quando o índice for criado. Ao se recalcular estatísticas retarda-se a criação dos índices, mas em geral melhora-se o desempenho da consulta.  
  
**Bloqueios de Linha Permitidos**  
Especifica se o bloqueio de linha é permitido no índice. A permissão ou não dos bloqueios de linha afeta o desempenho do banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
