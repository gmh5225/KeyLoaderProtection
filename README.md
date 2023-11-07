# KeyLoaderProtection
Do you want to have protection for your loader? like KeyAuth? This is for you !

BOOL anti_debugger()
{
	SPOOF_FUNC
	BOOL is_debugged = FALSE;
	HANDLE h_process = GetCurrentProcess();
	HANDLE h_snapshot = CreateToolhelp32Snapshot(TH32CS_SNAPALL, 0);
	PROCESSENTRY32 process_entry = { 0 };
	process_entry.dwSize = sizeof(PROCESSENTRY32);
	Process32First(h_snapshot, &process_entry);

	do
	{
		if (_stricmp(process_entry.szExeFile, "notepad.exe") == 0
			|| _stricmp(process_entry.szExeFile, "procexp.exe") == 0
			|| _stricmp(process_entry.szExeFile, "ollydbg.exe") == 0
			|| _stricmp(process_entry.szExeFile, "idaq.exe") == 0
			|| _stricmp(process_entry.szExeFile, "idaq64.exe") == 0
			|| _stricmp(process_entry.szExeFile, "UD.exe") == 0
			|| _stricmp(process_entry.szExeFile, "ImmunityDebugger.exe") == 0
			|| _stricmp(process_entry.szExeFile, "x64dbg.exe") == 0
			|| _stricmp(process_entry.szExeFile, "windbg.exe") == 0
			|| _stricmp(process_entry.szExeFile, "joeboxcontrol.exe") == 0)
		{
			is_debugged = TRUE;
			break;
		}
	} while (Process32Next(h_snapshot, &process_entry));

	CloseHandle(h_snapshot);
	if (is_debugged)
	{
		std::cout << "try me nigga.\n\n";
		Sleep(1000);
		TerminateProcess(h_process, 0);
		return TRUE;
	}

	return FALSE;
}
