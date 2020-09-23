---
title: Lista de bugs corrigidos
description: Esta página contém uma lista de bugs corrigidos em cada versão, começando com o Microsoft ODBC Driver 17 for SQL Server.
ms.custom: ''
ms.date: 04/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: v-chojas
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: fb686e3c70723cf847853ad558f47cf37da23972
ms.sourcegitcommit: bc10ec0be5ddfc5f0bc220a9ac36c77dd6b80f1d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2020
ms.locfileid: "87544299"
---
# <a name="list-of-bugs-fixed"></a>Lista de bugs corrigidos

Esta página contém uma lista de bugs corrigidos em cada versão, começando com o [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

### <a name="bug-fixes-in-the-msconame-odbc-driver-176-for-ssnoversion"></a>Correção de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.6 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correção de erro de ADAL ao autenticar com uma conta federada (Windows)
- Correção de um problema em que o driver não respondia quando ocorria um tempo limite durante uma operação de notificação assíncrona
- Correção da contagem de referência de driver na atualização no Alpine Linux
- Correção da versão de dependência de libc6 para Ubuntu
- Adição de definições ausentes no msodbcsql.h para Linux/Mac

### <a name="bug-fixes-in-the-msconame-odbc-driver-17522-for-ssnoversion-alpine-linux-only"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.5.2.2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (apenas Alpine Linux)

- Correção de uma falha ao usar o Always Encrypted com enclaves seguros no Alpine Linux

### <a name="bug-fixes-in-the-msconame-odbc-driver-1752-for-ssnoversion"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.5.2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- msodbcsql.h adicionado ao pacote Alpine do Linux

### <a name="bug-fixes-in-the-msconame-odbc-driver-175-for-ssnoversion"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.5 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correção do cálculo de hash de metadados do AKV CMK no Linux/macOS
- Correção de erro ao carregar o OpenSSL 1.0.0
- Correção de problemas de conversão ao usar as páginas de código ISO-8859-1 e ISO-8859-2
- Correção do nome da biblioteca interna no macOS para incluir o número de versão
- Correção da configuração do indicador nulo quando são usadas associações de comprimento e indicador separadas

### <a name="bug-fixes-in-the-msconame-odbc-driver-1742-for-ssnoversion"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.4.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

 - Correção para um problema em que a ID do processo e o nome do aplicativo não seriam enviados corretamente para o SQL Server (para análise sys.dm_exec_sessions) (Linux)
 - Remoção de dependência redundante no libuuid (Linux)
 - Correção de um bug com envio de dados UTF8 para o SQL Server 2019
 - Correção de um bug em que as localidades que terminam com "@euro" não estavam sendo corretamente detectadas (Linux)
 - Correção de dados XML que estão sendo retornados incorretamente quando obtidos como um parâmetro de saída durante o uso do Always Encrypted

### <a name="bug-fixes-in-the-msconame-odbc-driver-174-for-ssnoversion"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.4 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correção para o problema intermitente quando o MARS (conjunto de resultados ativos múltiplos) está habilitado em que o driver para de responder
- Correção do problema de resiliência da conexão quando a notificação assíncrona é habilitada em que o driver para de responder
- Correção de falha ao recuperar registros de diagnóstico para tentativas de conexão multithread
- Correção de "Criptografia não compatível" após a reconexão e depois de chamar SQLGetInfo() com SQL_USER_NAME e SQL_DATA_SOURCE_READ_ONLY
- Correção de erro de inicialização COM durante a Autenticação Interativa do Azure Active Directory
- Correção de SQLGetData () para dados UTF8 multibyte
- Correção da recuperação de comprimento de colunas sql_variant usando o SQLGetData ()
- Correção da importação de colunas sql_variant contendo mais de 7992 bytes usando bcp
- Correção do envio da codificação correta ao servidor para dados de caractere estreitos

### <a name="bug-fixes-in-the-msconame-odbc-driver-173-for-ssnoversion"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correção da perda de memória do manipulador de eventos de envio de TCP
- Correção do problema de redefinição da enumeração _SQL_FILESTREAM_DESIRED_ACCESS no arquivo de cabeçalho msodbcsql.h
- Correção da ausência de definição relacionada a ACCESS_TOKEN e a AUTHENTICATION no arquivo de cabeçalho msodbcsql.h para Linux

### <a name="bug-fixes-in-the-msconame-odbc-driver-172-for-ssnoversion"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correção de uma mensagem de erro sobre a Autenticação do Azure Active Directory
- Correção da detecção de codificação quando as variáveis de ambiente de localidade forem definidas de maneira diferente
- Correção de uma falha ao desconectar da recuperação da conexão em andamento
- Correção da detecção de atividade da conexão
- Correção da detecção incorreta de soquetes fechados
- Correção de uma espera infinita ao tentar lançar um identificador de instrução durante a falha de recuperação
- Correção do comportamento de desinstalação incorreto quando as versões 13 e 17 são instaladas no Windows
- Correção do comportamento de descriptografia em uma plataforma mais antiga do Windows (Windows 7, 8 e Server 2012)
- Correção de um problema de cache ao usar a Autenticação ADAL no Windows
- Correção de um problema que estava bloqueando e substituindo logs de rastreamento no Windows

### <a name="bug-fixes-in-the-msconame-odbc-driver-171-for-ssnoversion"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correção do atraso de 1 segundo ao chamar SQLFreeHandle com MARS habilitado e o atributo de conexão "Encrypt=yes"
- Correção de falha do erro 22003 no SQLGetData quando o tamanho do buffer passado é menor do que os dados que estão sendo recuperados (Windows)
- Correção de mensagens de erro ADAL truncadas
- Correção de um bug raro no Windows de 32 bits ao converter um número de ponto flutuante em um número inteiro
- Correção de um problema em que a inserção dupla no campo decimal com o Always Encrypted ativado retornava um erro de truncamento de dados
- Correção de um aviso no instalador do macOS
- Correção do envio de estado incorreto para o SQL Server durante a tentativa de Recuperação da Sessão quando a Resiliência da Conexão e o Pool de Conexões estão habilitados, fazendo com que a sessão seja descartada pelo servidor

### <a name="bug-fixes-in-the-msconame-odbc-driver-17-for-ssnoversion"></a>Correções de bugs no [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correção de bug em que a inserção em massa pode falhar com o erro "acesso negado" quando a autenticação Kerberos é usada
- Solução alternativa removida para um bug unixODBC presente na versão inferior a 2.3.1 (o driver dobrou o tamanho de determinados buffers passados para unixODBC)
- Correção da Resiliência da Conexão (reconexão), que parava de responder ao usar ColumnEncryption=enabled
- Correção do bug de criação de DSN no qual ao usar a opção "Autenticação Interativa do Active Directory", a janela de Autenticação do Azure poderia ficar sem resposta (Windows)
- Correção de uma falha rara durante o desligamento do ODBC quando uma execução assíncrona está habilitada (ocorrida ao limpar o identificador de conexão)
- Correção de um problema em que o Driver SQL causou alto consumo de CPU durante a execução de procedimentos armazenados longos
- Correção da incapacidade de recuperar dados em uma coluna varbinary(max) criptografada sem conversão
- Correção de um problema em que após uma coluna criptografada varchar(max) nula ser buscada usando SQLGetData() em um cursor estático, a coluna a seguir também é anulada, mesmo que ela tenha dados
- Correção de um problema com a busca do campo varbinary(max) com o Always Encrypted ativado
- Correção de um problema em que setlocale() não funciona com o Always Encrypted
- Correção de um problema com o erro de retorno do SQLDescribeParam() quando chamado no parâmetro de procedimento armazenado de tipo XML com o Always Encrypted ativado
- Correção de sublinhados de escape que não funcionam no SQLTables
- Correção de um bug em que os dados em Hebraico (varchar) são truncados quando retornados como caracteres amplos no Linux
- Correção de um problema com a consulta de caracteres/varchar codificados com Shift-JIS no aplicativo UTF-8
- Correção do bug em que chamar SQLGetInfo com o parâmetro SQL_DRIVER_NAME retornava um nome de arquivo no estilo Linux no macOS
- Correção de um problema em que carregar dados de caractere do Windows-1252, usando arquivos de entrada maiores do que 32 mil bytes em colunas VARCHAR usando o utilitário BCP resultaria em falhas
