---
title: Criar um alias de tipo de dados definido pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.userdefineddatatype.general.f1
- sql13.swb.new.datatype.properties.general.f1
helpviewer_keywords:
- alias data types [SQL Server], creating
ms.assetid: b1dd8413-0cd0-411b-a79b-1bb043ccc62d
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0aa09ddef11c733abda1a5e706c1b788c3745c8e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511881"
---
# <a name="create-a-user-defined-data-type-alias"></a>Criar um alias de tipo de dados definido pelo usuário
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico descreve como criar um novo alias de tipo de dados definido pelo usuário no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar um alias de tipo de dados definido pelo usuário, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O nome de um alias de tipo de dados definido pelo usuário deve estar de acordo com as regras para identificadores.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão CREATE TYPE no banco de dados atual e a permissão ALTER no *schema_name*. Se *schema_name* não for especificado, serão aplicadas as regras de resolução de nome padrão para determinar o esquema do usuário atual.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-user-defined-data-type"></a>Para criar um tipo de dados definido pelo usuário  
  
1.  No Pesquisador de Objetos, expanda **Bancos de dados**, expanda um banco de dados, expanda **Programação**, expanda **Tipos**, clique com o botão direito do mouse em **Tipos de Dados Definidos pelo Usuário**e clique em **Novo Tipo de Dados Definido pelo Usuário**.  
  
     **Permitir Nulos**  
     Especifique se o tipo de dados definido pelo usuário pode aceitar valores NULL. A nulidade de um tipo de dados definido pelo usuário existente não é editável.  
  
     **Data type**  
     Selecione o tipo de dados base na caixa de listagem. A caixa de listagem exibe todos os tipos de dados, com exceção do tipo de dados **geography**, **geometry**, **hierarchyid**, **sysname**, **timestamp** e **xml** . O tipo de dados definido pelo usuário existente não é editável.  
  
     **Default**  
     Opcionalmente, selecione um padrão para associar ao alias do tipo de dados definido pelo usuário.  
  
     **Comprimento/Precisão**  
     Exibe o comprimento ou a precisão do tipo de dados, conforme aplicável. **Tamanho** se aplica a tipos de dados definidos pelo usuário com base em caracteres; **Precisão** se aplica apenas a tipos de dados definidos pelo usuário com base numérica. O rótulo se altera dependendo do tipo de dados selecionado anteriormente. Essa caixa não será editável se o comprimento ou a precisão do tipo de dados selecionado for fixo.  
  
     O tamanho não é exibido para os tipos de dados **nvarchar(max)**, **varchar(max)** ou **varbinary(max)** .  
  
     **Nome**  
     Se você estiver criando um novo alias de tipo de dados definido pelo usuário, digite um nome exclusivo a ser usado no banco de dados para representar o tipo de dados definido pelo usuário. O número máximo de caracteres deve corresponder ao tipo de dados **sysname** do sistema. O nome de um alias de tipo de dados definido pelo usuário existente não é editável.  
  
     **Regra**  
     Opcionalmente, selecione uma regra para associar ao alias de tipo de dados definido pelo usuário.  
  
     **Escala**  
     Especifique o número máximo de dígitos decimais que podem ser armazenados à direita do ponto decimal.  
  
     **Esquema**  
     Selecione um esquema de uma lista de todos os esquemas disponíveis para o usuário atual. A seleção padrão é o esquema padrão do usuário atual.  
  
     **Armazenamento**  
     Exibe o tamanho de armazenamento máximo para o alias de tipo de dados definido pelo usuário. Os tamanhos máximos de armazenamento variam com base na precisão.  
  
    |||  
    |-|-|  
    |1 - 9|5|  
    |10 – 19|9|  
    |20 – 28|13|  
    |29 – 38|17|  
  
     Para tipos de dados **nchar** e **nvarchar** , o valor de armazenamento sempre é duas vezes o valor de **Comprimento**.  
  
     O armazenamento não é exibido para os tipos de dados **nvarchar(max)**, **varchar(max)** ou **varbinary(max)** .  
  
2.  Na caixa de diálogo **Tipo de Dados Definido pelo Usuário** , na caixa **Esquema** , digite o esquema próprio para esse alias de tipo de dados ou use o botão Procurar para selecionar o esquema.  
  
3.  Na caixa **Nome** , digite um nome para o novo alias de tipo de dados.  
  
4.  Na caixa **Tipo de dados** , selecione o tipo de dados que servirá de base para o novo alias de tipo de dados.  
  
5.  Complete as caixas **Tamanho**, **Precisão**e **Escala** caso seja adequado para aquele tipo de dados.  
  
6.  Marque **Permitir NULLs** , se o novo alias de tipo de dados puder permitir valores NULL.  
  
7.  Na área **Associação** , preencha a caixa **Padrão** ou **Regra** caso queira associar um padrão ou uma regra ao novo alias de tipo de dados. Padrões e regras não podem ser criados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Use [!INCLUDE[tsql](../../includes/tsql-md.md)]. Código de exemplo para criação de padrões e regras disponíveis no Explorador de Modelos.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-user-defined-data-type-alias"></a>Para criar um alias de tipo de dados definido pelo usuário  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo cria um alias de tipo de dados com base no tipo de dados `varchar` fornecido pelo sistema. O alias de tipo de dados `ssn` é usado para colunas contendo números de previdência social de 11 dígitos (999-99-9999). A coluna não pode ser NULL.  
  
```sql  
CREATE TYPE ssn  
FROM varchar(11) NOT NULL ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Identificadores de banco de dados](../../relational-databases/databases/database-identifiers.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)  
  
  
