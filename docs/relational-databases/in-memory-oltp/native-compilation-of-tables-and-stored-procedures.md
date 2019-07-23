---
title: Compilação nativa de tabelas e procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 04/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5880fbd9-a23e-464a-8b44-09750eeb2dad
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 09e1e143f22c36e66670f9c02590e009e939a048
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101440"
---
# <a name="native-compilation-of-tables-and-stored-procedures"></a>Compilação nativa de tabelas e procedimentos armazenados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
O OLTP na memória apresenta o conceito de compilação nativa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode compilar nativamente procedimentos armazenados que acessam tabelas com otimização de memória. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também pode compilar nativamente tabelas com otimização de memória. A compilação nativa permite o acesso mais rápido a dados e a execução mais eficiente de consultas, em comparação ao [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado (tradicional). A compilação nativa de tabelas e procedimentos armazenados gera DLLs.

A compilação nativa de tipos de tabelas com otimização de memória também tem suporte. Para obter mais informações, consulte [Tabela temporária e variável de tabela mais rápidas usando a otimização de memória](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md).

A compilação nativa refere-se ao processo de converter construções de programação em código nativo, que consiste em instruções de processador, dispensando compilação ou interpretação adicional.

OLTP em memória compila tabelas com otimização de memória quando elas são criadas e procedimentos armazenados compilados nativamente quando são carregados para DLLs nativos. Além disso, as DLLs são recompiladas após a reinicialização de um banco de dados ou servidor. As informações necessárias para recriar as DLLs são armazenadas nos metadados do banco de dados. As DLLs não fazem parte do banco de dados, embora elas estejam associadas ao banco de dados. Por exemplo, as DLLs não são incluídas nos backups de bancos de dados.

> [!NOTE]
> Tabelas com otimização de memória são recompiladas durante uma reinicialização do servidor. Para acelerar a recuperação do banco de dados, procedimentos armazenados compilados nativamente não são recompilados durante uma reinicialização do servidor, mas no momento da primeira execução. Como resultado dessa compilação adiada, procedimentos de armazenamento compilados nativamente aparecem apenas ao chamar [sys.dm_os_loaded_modules &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql.md) após a primeira execução.

## <a name="maintenance-of-in-memory-oltp-dlls"></a>Manutenção das DLLs do OLTP na memória

A consulta a seguir mostra todas as DLLs de tabela e procedimento armazenado atualmente carregadas na memória do servidor.

```sql
SELECT
        mod1.name,
        mod1.description
    from
        sys.dm_os_loaded_modules  as mod1
    where
        mod1.description = 'XTP Native DLL';
```

Os administradores de banco de dados não precisam manter os arquivos gerados por um compilação nativa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remove automaticamente os arquivos gerados que não são mais necessários. Por exemplo, os arquivos gerados serão excluídos quando uma tabela e um procedimento armazenado forem excluídos, ou se um banco de dados for descartado.

> [!NOTE]
> Se a compilação falhar ou for interrompida, alguns arquivos gerados não serão removidos. Esses arquivos são deixados para trás intencionalmente, por questões de capacidade de suporte, e são removidos quando o banco de dados é descartado.

> [!NOTE]
> O SQL Server compila DLLs para todas as tabelas necessárias para a recuperação de banco de dados. Se uma tabela foi descartada logo antes de uma reinicialização do banco de dados, ainda pode haver resíduos da tabela nos arquivos do ponto de verificação ou no log de transações, de modo que a DLL para a tabela pode ser recompilada durante a inicialização do banco de dados. Após a reinicialização, a DLL será descarregada e os arquivos serão removidos pelo processo normal de limpeza.

## <a name="native-compilation-of-tables"></a>Compilação nativa de tabelas

A criação de uma tabela com otimização de memória usando a instrução **CREATE TABLE** faz com que as informações da tabela sejam gravadas nos metadados do banco de dados, bem como nas estruturas de tabela e índice criadas na memória. A tabela também será compilada em uma DLL.

Considere o script de exemplo a seguir, que cria um banco de dados e uma tabela com otimização de memória:

```sql
USE master;
GO

CREATE DATABASE DbMemopt3;
GO

ALTER DATABASE DbMemopt3
    add filegroup DbMemopt3_mod_memopt_1_fg
        contains memory_optimized_data
;
GO

-- You must edit the front portion of filename= path, to where your DATA\ subdirectory is,
-- keeping only the trailing portion '\DATA\DbMemopt3_mod_memopt_1_fn'!

ALTER DATABASE DbMemopt3
    add file
    (
        name     = 'DbMemopt3_mod_memopt_1_name',
        filename = 'C:\DATA\DbMemopt3_mod_memopt_1_fn'

        --filename = 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQLSVR2016ID\MSSQL\DATA\DbMemopt3_mod_memopt_1_fn'
    )
        to filegroup DbMemopt3_mod_memopt_1_fg
;
GO

USE DbMemopt3;
GO

CREATE TABLE dbo.t1
(
    c1 int not null primary key nonclustered,
    c2 int
)
    with (memory_optimized = on)
;
GO



-- You can safely rerun from here to the end.

-- Retrieve the path of the DLL for table t1.


DECLARE @moduleName  nvarchar(256);

SET @moduleName =
    (
        '%xtp_t_' +
        cast(db_id() as nvarchar(16)) +
        '_' +
        cast(object_id('dbo.t1') as nvarchar(16)) +
        '%.dll'
    )
;


-- SEARCHED FOR NAME EXAMPLE:  mod1.name LIKE '%xtp_t_8_565577053%.dll'
PRINT @moduleName;


SELECT
        mod1.name,
        mod1.description
    from
        sys.dm_os_loaded_modules  as mod1
    where
        mod1.name LIKE @moduleName
    order by
        mod1.name
;
-- ACTUAL NAME EXAMPLE:  mod1.name = 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQLSVR2016ID\MSSQL\DATA\xtp\8\xtp_t_8_565577053_184009305855461.dll'
GO

--   DROP DATABASE DbMemopt3;  -- Clean up.
GO
```

A criação da tabela também cria a DLL de tabela e a carrega na memória. A consulta DMV imediatamente após a instrução CREATE TABLE recupera o caminho da DLL de tabela.

A DLL de tabela entende as estruturas de índice e o formato da linha da tabela. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a DLL para percorrer índices, recuperar linhas e armazenar o conteúdo das linhas.

## <a name="native-compilation-of-stored-procedures"></a>Compilação nativa de procedimentos armazenados

Os procedimentos armazenados que são marcados com NATIVE_COMPILATION são compilados nativamente. Isso significa que as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] no procedimento são todas compiladas em código nativo para execução eficiente da lógica de negócios crítica ao desempenho.

Para obter mais informações sobre procedimentos armazenados nativamente compilados, consulte [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).

Considere o procedimento armazenado do exemplo a seguir, que insere linhas na tabela t1 do exemplo anterior:

```sql
CREATE PROCEDURE dbo.native_sp
    with native_compilation,
         schemabinding,
         execute as owner
as
begin atomic
    with (transaction isolation level = snapshot,
          language = N'us_english')

    DECLARE @i int = 1000000;

    WHILE @i > 0
    begin
        INSERT dbo.t1 values (@i, @i+1);
        SET @i -= 1;
    end
end;
GO

EXECUTE dbo.native_sp;
GO

-- Reset.

DELETE from dbo.t1;
GO
```

A DLL para native_sp pode interagir diretamente com a DLL para t1, bem como com o mecanismo de armazenamento do OLTP na memória, para inserir as linhas o mais rápido possível.

O compilador do OLTP na memória aproveita o otimizador de consulta para criar um plano de execução eficiente para cada uma das consultas no procedimento armazenado. Observe que os procedimentos armazenados compilados nativamente serão recompilados automaticamente se os dados na tabela forem alterados. Para obter mais informações sobre como manter estatísticas e procedimentos armazenados com OLTP in-memory, consulte [Estatísticas para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md).

## <a name="security-considerations-for-native-compilation"></a>Considerações de segurança para compilação nativa

A compilação nativa de tabelas e procedimentos armazenados usa o compilador OLTP na memória. Esse compilador gera arquivos que são gravados no disco e carregados na memória. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa os seguintes mecanismos para limitar o acesso a esses arquivos.

### <a name="native-compiler"></a>Compilador nativo

O executável do compilador, bem como os binários e os arquivos de cabeçalho necessários à compilação nativa são instalados como parte da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na pasta MSSQL\Binn\Xtp. Portanto, se a instância padrão for instalada em C:\Arquivos de Programas, os arquivos do compilador serão instalados em C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\Binn\Xtp.

Para limitar o acesso ao compilador, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use listas de controle de acesso (ACLs) para restringir o acesso aos arquivos binários. Todos os binários do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são protegidos contra a modificação ou violação através de ACLs. As ACLs do compilador nativo também limitam o uso do compilador; somente os administradores de sistema e de conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm permissões de leitura e execução nos arquivos do compilador nativo.

### <a name="files-generated-by-a-native-compilation"></a>Arquivos gerados por uma compilação nativa

Os arquivos gerados quando uma tabela ou um procedimento armazenado é compilado são arquivos DLL e intermediários que incluem arquivos com as seguintes extensões: .c, .obj, .xml, e .pdb. Os arquivos gerados são salvos em uma subpasta da pasta de dados padrão. A subpasta é chamada Xtp. Ao instalar a instância padrão com a pasta de dados padrão, os arquivos gerados são colocados em C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\DATA\Xtp.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] evita a violação das DLLs geradas de três maneiras:

- Quando uma tabela ou um procedimento armazenado é compilado em uma DLL, esta é carregada imediatamente na memória e vinculada ao processo do sqlserver.exe. Uma DLL não pode ser modificada enquanto está vinculada a um processo.

- Quando um banco de dados é reinicializado, todas as tabelas e procedimentos armazenados são recompilados (removidos e recriados) com base nos metadados do banco de dados. Isso removerá todas as alterações feitas em um arquivo gerado por um agente mal-intencionado.

- Os arquivos gerados são considerados parte dos dados do usuário e têm as mesmas restrições de segurança, via ACLs, que arquivos de banco de dados: somente os administradores de sistema e de conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem acessar esses arquivos.

Nenhuma interação do usuário é necessária para gerenciar esses arquivos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criará e removerá os arquivos conforme necessário.

## <a name="see-also"></a>Consulte Também

[Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)

[Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)
