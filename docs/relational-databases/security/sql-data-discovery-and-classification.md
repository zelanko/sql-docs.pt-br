---
title: Descoberta e classificação de dados SQL | Microsoft Docs
description: Descoberta e classificação de dados SQL
documentationcenter: ''
ms.reviewer: vanto
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.prod_service: sql-database,sql
ms.custom: security
ms.topic: conceptual
ms.date: 06/10/2020
ms.author: datrigan
author: DavidTrigano
ms.openlocfilehash: 7c23b7faa93281ab34ed4b500d10dfd50e9c8c76
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85737037"
---
# <a name="sql-data-discovery-and-classification"></a>Descoberta e classificação de dados SQL
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

O recurso Descoberta e Classificação de Dados apresenta uma nova ferramenta interna do [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para **descobrir**, **classificar**, **rotular** & **e relatar** os dados confidenciais em seus bancos de dados.
A descoberta e a classificação dos dados mais confidenciais (de negócios, financeiros, de serviços de saúde, etc.) podem desempenhar um papel fundamental na dimensão da proteção de informações organizacionais. Esse recurso pode funcionar como a infraestrutura para:
* Ajudar a atender aos padrões de privacidade de dados.
* Controlar o acesso a e fortalecer a segurança de bancos de dados/colunas que contêm dados altamente confidenciais.

> [!NOTE]
> O recurso Descoberta e Classificação de Dados é **compatível com o SQL Server 2012 ou posterior, podendo ser usado com o [SSMS 17.5](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) ou posterior**. Para o Banco de Dados SQL do Azure, confira [Descoberta e Classificação de Dados do Banco de Dados SQL do Azure](/azure/sql-database/sql-database-data-discovery-and-classification/).

## <a name="overview"></a><a id="subheading-1"></a>Visão geral
O recurso Descoberta e classificação de dados apresenta um conjunto de serviços avançados, formando um novo paradigma de Proteção de Informações do SQL que visa a proteção dos dados, não apenas do banco de dados:

* **Descoberta e recomendações** – o mecanismo de classificação verifica o banco de dados e identifica colunas que contenham dados possivelmente confidenciais. Em seguida, ele fornece uma maneira fácil de examinar e aplicar as recomendações de classificação apropriada, bem como de classificar as colunas manualmente.
* **Definição de rótulos** – rótulos de classificação de confidencialidade podem ser marcados com persistência em colunas.
* **Visibilidade** – o estado de classificação do banco de dados pode ser exibido em um relatório detalhado que pode ser impresso/exportado para ser usado para fins de auditoria e conformidade, bem como para outras necessidades.

## <a name="discovering-classifying--labeling-sensitive-columns"></a><a id="subheading-2"></a>Descobrindo, classificando e rotulando colunas confidenciais
A seção a seguir descreve as etapas para descobrir, classificar e rotular colunas que contenham dados confidenciais no banco de dados, bem como exibir o estado atual de classificação do banco de dados e exportar relatórios.

A classificação inclui dois atributos de metadados:
* Rótulos – os atributos de classificação principais, usados para definir o nível de confidencialidade dos dados armazenados na coluna.  
* Tipos de informações – fornecem uma granularidade adicional para o tipo dos dados armazenados na coluna.

**Para classificar o banco de dados do SQL Server:**

1. No SSMS (SQL Server Management Studio), conecte-se ao SQL Server.

2. No Pesquisador de Objetos do SSMS, clique com o botão direito do mouse no banco de dados que deseja classificar e escolha **Tarefas** > **Descoberta e Classificação de Dados** > **Classificar Dados...** .

   ![Painel de navegação][0]

3. O mecanismo de classificação verifica o banco de dados em busca de colunas que contenham dados possivelmente confidenciais e fornece uma lista de **classificações de coluna recomendadas**:

    * Para exibir a lista de classificações de coluna recomendadas, clique na caixa de notificação de recomendações na parte superior ou no painel de recomendações na parte inferior da janela:

        ![Painel de navegação][2]

        ![Painel de navegação][3]

    * Examine a lista de recomendações:
        * Para aceitar uma recomendação para uma coluna específica, marque a caixa de seleção na coluna à esquerda da linha relevante. Você também pode marcar *todas as recomendações* como aceitas, marcando a caixa de seleção no cabeçalho da tabela de recomendações.

        * Também é possível alterar o tipo de informações e o rótulo de confidencialidade recomendados usando as caixas suspensas.        

        ![Painel de navegação][4]

    * Para aplicar as recomendações selecionadas, clique no botão **Aceitar recomendações selecionadas** azul.

        ![Painel de navegação][5]

4. Você também pode **classificar manualmente** as colunas como uma alternativa ou, além da classificação de recomendação:

    * Clicar em **Adicionar classificação** no menu superior da janela.

        ![Painel de navegação][6]

    * Na janela de contexto que é aberta, selecionar o esquema > a tabela > a coluna que você deseja classificar e, em seguida, o tipo de informações e o rótulo confidencialidade. Em seguida, clicar no botão **Adicionar classificação** azul na parte inferior da janela do contexto.

        ![Painel de navegação][7]

5. Para concluir sua classificação e definir um rótulo (uma marca) persistente para as colunas do banco de dados com os novos metadados de classificação, clique em **Salvar** no menu superior da janela.

    ![Painel de navegação][8]


6. Para gerar um relatório com um resumo completo do estado de classificação do banco de dados, clique em **Exibir Relatório** no menu superior da janela. (Você também pode gerar um relatório usando o SSMS. Clique com o botão direito do mouse no banco de dados em que deseja gerar o relatório e escolha **Tarefas** > **Descoberta e Classificação de Dados** > **Gerar Relatório...** )

    ![Painel de navegação][9]

    ![Painel de navegação][10]

## <a name="manage-information-protection-policy-with-ssms"></a><a id="subheading-3"></a>Gerenciar a política de proteção de informações com o SSMS

Gerencie a política de proteção de informações usando o [SSMS 18.4](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) ou posterior:

1. No SSMS (SQL Server Management Studio), conecte-se ao SQL Server.

2. No Pesquisador de Objetos do SSMS, clique com o botão direito do mouse em um dos bancos de dados e escolha **Tarefas** > **Descoberta e Classificação de Dados**.

   As seguintes opções de menu permitem que você gerencie a política de proteção de informações:

* **Definir o Arquivo da Política de Proteção de Informações**: usa a política de proteção de informações, conforme definido no arquivo JSON selecionado.

* **Exportar a Política de Proteção de Informações**: exporta a política de proteção de informações para um arquivo JSON.

* **Redefinir a Política de Proteção de Informações**: redefine a política de proteção de informações para a política de proteção de informações padrão.

> [!IMPORTANT]
> O arquivo da política de proteção de informações não é armazenado no SQL Server.
> O SSMS usa uma política de proteção de informações padrão. Se uma política de proteção de informações personalizada falhar, o SSMS não poderá usar a política padrão. A classificação de dados falha. Para resolver isso, clique em **Redefinir a Política de Proteção de Informações** para usar a política padrão e habilitar a classificação de dados novamente.

## <a name="accessing-the-classification-metadata"></a><a id="subheading-4"></a>Acessando os metadados de classificação

O SQL Server 2019 apresenta a exibição do catálogo do sistema [`sys.sensitivity_classifications`](../system-catalog-views/sys-sensitivity-classifications-transact-sql.md). Essa exibição retorna tipos de informações e rótulos de confidencialidade. 

> [!NOTE]
> Essa exibição exige a permissão **VIEW ANY SENSITIVITY CLASSIFICATION**. Para obter mais informações, consulte [Metadata Visibility Configuration](https://docs.microsoft.com/sql/relational-databases/security/metadata-visibility-configuration?view=sql-server-ver15).

Nas instâncias do SQL Server 2019, consulte `sys.sensitivity_classifications` para examinar todas as colunas classificadas com as classificações correspondentes. Por exemplo: 

```sql
SELECT 
    schema_name(O.schema_id) AS schema_name,
    O.NAME AS table_name,
    C.NAME AS column_name,
    information_type,
    label,
    rank,
    rank_desc
FROM sys.sensitivity_classifications sc
    JOIN sys.objects O
    ON  sc.major_id = O.object_id
    JOIN sys.columns C 
    ON  sc.major_id = C.object_id  AND sc.minor_id = C.column_id
```

Antes do SQL Server 2019, os metadados de classificação para tipos de informações e rótulos de confidencialidade estão localizados nas seguintes Propriedades Estendidas: 

* `sys_information_type_name`
* `sys_sensitivity_label_name`

Os metadados podem ser acessados usando a exibição do catálogo [`sys.extended_properties`](../system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md) das Propriedades Estendidas.

Para as instâncias do SQL Server 2017 e anterior, o seguinte exemplo retorna todas as colunas classificadas com as classificações correspondentes:

```sql
SELECT
    schema_name(O.schema_id) AS schema_name,
    O.NAME AS table_name,
    C.NAME AS column_name,
    information_type,
    sensitivity_label 
FROM
    (
        SELECT
            IT.major_id,
            IT.minor_id,
            IT.information_type,
            L.sensitivity_label 
        FROM
        (
            SELECT
                major_id,
                minor_id,
                value AS information_type 
            FROM sys.extended_properties 
            WHERE NAME = 'sys_information_type_name'
        ) IT 
        FULL OUTER JOIN
        (
            SELECT
                major_id,
                minor_id,
                value AS sensitivity_label 
            FROM sys.extended_properties 
            WHERE NAME = 'sys_sensitivity_label_name'
        ) L 
        ON IT.major_id = L.major_id AND IT.minor_id = L.minor_id
    ) EP
    JOIN sys.objects O
    ON  EP.major_id = O.object_id 
    JOIN sys.columns C 
    ON  EP.major_id = C.object_id AND EP.minor_id = C.column_id
```

## <a name="manage-classifications"></a><a id="subheading-5"></a>Gerenciar classificações

# <a name="t-sql"></a>[T-SQL](#tab/t-sql)
Você pode usar o T-SQL para adicionar/remover classificações de coluna, bem como para recuperar todas as classificações para o banco de dados inteiro.

- Adicione/atualize a classificação de uma ou mais colunas: [ADD SENSITIVITY CLASSIFICATION](https://docs.microsoft.com/sql/t-sql/statements/add-sensitivity-classification-transact-sql)
- Remova a classificação de uma ou mais colunas: [DROP SENSITIVITY CLASSIFICATION](https://docs.microsoft.com/sql/t-sql/statements/drop-sensitivity-classification-transact-sql)

# <a name="powershell-cmdlet"></a>[Cmdlet do PowerShell](#tab/sql-powelshell)
Use o cmdlet do PowerShell para adicionar/remover classificações de coluna, bem como para recuperar todas as classificações e obter recomendações para todo o banco de dados.

- [Get-SqlSensitivityClassification](https://docs.microsoft.com/powershell/module/sqlserver/Get-SqlSensitivityClassification?view=sqlserver-ps)
- [Get-SqlSensitivityRecommendations](https://docs.microsoft.com/powershell/module/sqlserver/Get-SqlSensitivityRecommendations?view=sqlserver-ps)
- [Set-SqlSensitivityClassification](https://docs.microsoft.com/powershell/module/sqlserver/Set-SqlSensitivityClassification?view=sqlserver-ps)
- [Remove-SqlSensitivityClassification](https://docs.microsoft.com/powershell/module/sqlserver/Remove-SqlSensitivityClassification?view=sqlserver-ps)

---

## <a name="next-steps"></a><a id="subheading-6"></a>Próximas etapas

Para o Banco de Dados SQL do Azure, confira [Descoberta e Classificação de Dados do Banco de Dados SQL do Azure](https://go.microsoft.com/fwlink/?linkid=866265).

Considere proteger suas colunas confidenciais aplicando mecanismos de segurança no nível da coluna:

* [Máscara de Dados Dinâmicos](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking) para ofuscar as colunas confidenciais em uso.
* [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) para criptografar as colunas confidenciais em repouso.

<!--Anchors-->
[SQL Data Discovery & Classification overview]: #subheading-1
[Discovering, classifying & labeling sensitive columns]: #subheading-2
[Manage information protection policy with SSMS]: #subheading-3
[Accessing the classification metadata]: #subheading-4
[Manage classifications]: #subheading-5
[Next Steps]: #subheading-6

<!--Image references-->

[0]: ./media/sql-data-discovery-and-classification/0-data-classification-explorer.png
[2]: ./media/sql-data-discovery-and-classification/2-recommendations-notification-box.png
[3]: ./media/sql-data-discovery-and-classification/3-recommendations-panel.png
[4]: ./media/sql-data-discovery-and-classification/4-recommendations.png
[5]: ./media/sql-data-discovery-and-classification/5-accept-recommendations-button.png
[6]: ./media/sql-data-discovery-and-classification/6-add-classification-button.png
[7]: ./media/sql-data-discovery-and-classification/7-manual-classification.png
[8]: ./media/sql-data-discovery-and-classification/8-save.png
[9]: ./media/sql-data-discovery-and-classification/9-view-report.png
[10]: ./media/sql-data-discovery-and-classification/10-report.png
