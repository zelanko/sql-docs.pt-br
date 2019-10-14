---
title: Lista de bugs corrigidos | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 2b939db6ac0f89075b39ba74eadb0e86e63e3980
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041216"
---
# <a name="list-of-bugs-fixed"></a>Lista de bugs corrigidos

Esta página contém uma lista de bugs corrigidos em cada versão, começando com o [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-1742-for-includessnoversionincludesssnoversion-mdmd"></a>Correções de bugs no driver ODBC [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17.4.2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

 - Correção para um problema em que a ID do processo e o nome do aplicativo não seriam enviados corretamente para SQL Server (para análise de sys. dm _exec_sessions) (Linux)
 - Dependência redundante removida em libuuid (Linux)
 - Correção para um bug com envio de dados UTF8 para SQL Server 2019
 - Correção para um bug em que as localidades que terminam em "@euro" não estavam sendo corretamente detectadas (Linux)
 - Correção para dados XML que estão sendo retornados incorretamente quando obtidos como um parâmetro de saída durante o uso de Always Encrypted

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-174-for-includessnoversionincludesssnoversion-mdmd"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] driver ODBC 17,4 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correção para interrupção intermitente quando vários MARS (conjuntos de resultados ativos) estiverem habilitados
- Corrigir resiliência de conexão trava quando a notificação assíncrona está habilitada
- Correção de falha ao recuperar registros de diagnóstico para tentativas de conexão multi-threaded
- Corrigir ' criptografia sem suporte ' após a reconexão após chamar SQLGetInfo () com SQL_USER_NAME e SQL_DATA_SOURCE_READ_ONLY
- Corrigir erro de inicialização COM durante Azure Active Directory autenticação interativa
- Corrigir SQLGetData () para dados UTF8 de vários bytes
- Corrigir a recuperação de comprimento de colunas sql_variant usando SQLGetData ()
- Corrigir a importação de colunas sql_variant contendo mais de 7992 bytes usando bcp
- Corrigir o envio de codificação correta ao servidor para dados de caracteres estreitos

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] driver ODBC 17,3 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Corrigido o vazamento de memória do identificador de evento de notificação de envio TCP
- Corrigido o problema de redefinição de enumeração _SQL_FILESTREAM_DESIRED_ACCESS no arquivo de cabeçalho msodbcsql. h
- Correção de ACCESS_TOKEN ausente e definição relacionada à autenticação no arquivo de cabeçalho msodbcsql. h para Linux

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] driver ODBC 17,2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correção de uma mensagem de erro sobre a autenticação Azure Active Directory
- Correção da detecção de codificação quando as variáveis de ambiente de localidade são definidas de forma diferente
- Correção de uma falha após desconexão com a recuperação da conexão em andamento
- Detecção fixa da vida útil da conexão
- Correção da detecção incorreta de soquetes fechados
- Correção de uma espera infinita ao tentar liberar um identificador de instrução durante a recuperação com falha
- Corrigido o comportamento de desinstalação incorreto quando as versões 13 e 17 estiverem instaladas no Windows
- Correção do comportamento de descriptografia na plataforma mais antiga do Windows (Windows 7, 8 e Server 2012)
- Correção de um problema de cache ao usar a autenticação de ADAL no Windows
- Correção de um problema que estava bloqueando e substituindo os logs de rastreamento no Windows

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] driver ODBC 17,1 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Corrigido um atraso de 1 segundo ao chamar SQLFreeHandle com MARS habilitado e atributo de conexão "ENCRYPT = yes"
- Correção de um erro 22003 falha em SQLGetData quando o tamanho do buffer passado é menor que os dados que estão sendo recuperados (Windows)
- Mensagens de erro de ADAL truncadas corrigidas
- Correção de um bug raro em janelas de 32 bits ao converter um número de ponto flutuante em um número inteiro
- Corrigido um problema em que a inserção de Double em campo decimal com Always Encrypted em retornará um erro de truncamento de dados
- Correção de um aviso no MacOS Installer
- Corrigido o envio de estado incorreto para SQL Server durante a tentativa de recuperação de sessão quando a resiliência de conexão e o pool de conexões estão habilitados, fazendo com que a sessão seja descartada pelo servidor

### <a name="bug-fixes-in-the-includemsconameincludesmsconame_mdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correção de um bug em que, ao usar a autenticação Kerberos, a inserção em massa pode falhar com o erro "acesso negado"
- Foi removida a solução alternativa para um bug unixODBC presente na versão anterior 2.3.1 (o driver dobra os tamanhos de determinados buffers passados para unixODBC)
- Correção da resiliência de conexão (reconexão) suspensa ao usar ColumnEncryption = Enabled
- Corrigido o bug de criação de DSN, no qual ao usar a opção "autenticação interativa" Active Directory janela de autenticação do Azure poderia ficar sem resposta (Windows)
- Correção de uma falha rara durante o desligamento do ODBC quando a execução assíncrona estiver habilitada (ocorreu ao limpar o identificador de conexão)
- Corrigido um problema em que o driver SQL causou alto consumo de CPU durante a execução de procedimentos armazenados longos
- Correção da incapacidade de recuperar dados em uma coluna varbinary (max) criptografada sem conversão
- Corrigido um problema em que depois que uma coluna criptografada varchar (max) nula é buscada usando SQLGetData () em um cursor estático, a seguinte coluna também é nula, mesmo que ela tenha dados
- Corrigido um problema com a busca do campo varbinary (max) com Always Encrypted em
- Corrigido um problema de setlocale () que não funciona com Always Encrypted
- Corrigido um problema com o erro de retorno de SQLDescribeParam () quando chamado no parâmetro de procedimento armazenado de tipo XML com Always Encrypted em
- Sublinhados de escape corrigidos não funcionam em SQLTables
- Corrigido um bug em que os dados em Hebraico (varchar) são truncados quando retornados como caracteres largos no Linux
- Correção de um problema com a consulta de caracteres codificados com Shift-JIS no aplicativo UTF-8
- Corrigido o bug em que chamar SQLGetInfo com o parâmetro SQL_DRIVER_NAME retornou um nome de arquivo do estilo Linux no MacOS
- Corrigido um problema em que carregar dados de caractere do Windows-1252, usando arquivos de entrada maiores que 32K bytes em colunas VARCHAR usando o utilitário BCP resultaria em falhas
