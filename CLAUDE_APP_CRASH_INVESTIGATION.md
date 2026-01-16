# Claude AI App Crash Investigation Report

**Date:** November 24, 2025  
**App Version:** 0.14.10  
**macOS Version:** 12.7.6 (Monterey)  
**System:** Mac Mini

## Summary

The Claude AI desktop app is experiencing repeated crashes. The app has crashed multiple times in the past hour, with launchd reporting "service has crashed 1 times in a row" for processes 89549, 90242, and 90281. The app is currently running (process 90390) but has a history of instability.

## Key Findings

### 1. LaunchServices Timeout Errors
**Critical Issue:** Multiple instances of `LSExceptions shared instance invalidated for timeout` errors appear in the logs before each crash:

```
2025-11-24 13:27:21.744231+0100  localhost Claude[89549]: (LaunchServices) [com.apple.launchservices:default] LSExceptions shared instance invalidated for timeout.
2025-11-24 13:27:45.312934+0100  localhost Claude[89549]: (LaunchServices) [com.apple.launchservices:default] LSExceptions shared instance invalidated for timeout.
```

This pattern repeats before each crash, suggesting the crashes are related to LaunchServices communication failures.

### 2. Crash Pattern
- **Process 89549:** Crashed around 13:28:01
- **Process 90242:** Crashed around 13:29:54
- **Process 90281:** Crashed around 13:31:54
- **Process 90390:** Currently running (started 13:32:05)

Each crash follows a similar pattern: LaunchServices timeout errors, then the service becomes inactive and is removed by launchd.

### 3. System Resources
- **Memory Usage:** ~517 MB RSS (reasonable, not excessive)
- **Total System Memory:** 8 GB
- **No OOM Kills:** No evidence of memory-related crashes
- **App Data Size:** ~70 MB in Application Support

### 4. Missing Crash Reports
No crash reports found in `~/Library/Logs/DiagnosticReports/`, which suggests:
- The app may be terminating gracefully but unexpectedly
- Crash reports may be sent to Anthropic's crash reporting service
- The crashes might be caught and handled internally

## Root Cause Analysis

The **LaunchServices timeout errors** are the most likely root cause. LaunchServices is a macOS framework that handles:
- Application registration
- File type associations
- URL scheme handling
- Application launching coordination

When LaunchServices times out, it can cause applications to:
1. Fail to register properly
2. Lose access to system services
3. Experience communication failures with the system
4. Crash or become unresponsive

## Potential Causes

1. **macOS 12.7.6 Compatibility Issues**
   - Older macOS version may have compatibility issues with newer Electron-based apps
   - LaunchServices behavior may differ from newer macOS versions

2. **Corrupted LaunchServices Database**
   - The LaunchServices database may be corrupted
   - This can cause timeouts and communication failures

3. **System Resource Contention**
   - Other applications may be competing for LaunchServices resources
   - System load may be causing timeouts

4. **App-Specific Issues**
   - The app may be making too many LaunchServices calls
   - There may be a bug in how the app interacts with LaunchServices

## Recommended Solutions

### Immediate Actions (Try First)

1. **Rebuild LaunchServices Database**
   ```bash
   /System/Library/Frameworks/CoreServices.framework/Frameworks/LaunchServices.framework/Support/lsregister -kill -r -domain local -domain system -domain user
   ```
   Then restart your Mac.

2. **Clear Claude App Cache**
   ```bash
   rm -rf ~/Library/Application\ Support/Claude/Cache/*
   rm -rf ~/Library/Caches/com.anthropic.claudefordesktop/*
   ```

3. **Reset Claude Preferences**
   ```bash
   defaults delete com.anthropic.claudefordesktop
   ```

4. **Reinstall Claude App**
   - Quit Claude completely
   - Delete `/Applications/Claude.app`
   - Download and reinstall from Anthropic's website

### System-Level Fixes

5. **Update macOS** (if possible)
   - macOS 12.7.6 is quite old
   - Consider updating to a newer version if your Mac supports it
   - Newer versions have improved LaunchServices stability

6. **Check System Integrity**
   ```bash
   sudo /usr/libexec/repair_packages --verify --standard-pkgs /
   ```

7. **Reset NVRAM/PRAM**
   - Shut down your Mac
   - Turn it on and immediately hold Option + Command + P + R
   - Hold for about 20 seconds, then release

### Monitoring

8. **Monitor LaunchServices Activity**
   ```bash
   log stream --predicate 'subsystem == "com.apple.launchservices"' --level debug
   ```

9. **Check for Other LaunchServices Issues**
   ```bash
   log show --predicate 'eventMessage contains "LSExceptions"' --last 24h --style syslog | grep -v Claude
   ```

## Workaround

If crashes continue, you can:
- Use Claude via the web interface (claude.ai) instead of the desktop app
- Restart the app when it crashes (it appears to auto-restart via launchd)
- Monitor the app and restart it manually when LaunchServices errors appear

## Next Steps

1. Try the immediate actions above, starting with rebuilding the LaunchServices database
2. Monitor the app for 24-48 hours after applying fixes
3. If issues persist, contact Anthropic support with:
   - This investigation report
   - System logs showing LaunchServices timeouts
   - macOS version and Mac model information

## Additional Information

- **App Location:** `/Applications/Claude.app`
- **User Data:** `~/Library/Application Support/Claude/`
- **Preferences:** `~/Library/Preferences/com.anthropic.claudefordesktop.plist`
- **Crash Reports:** `~/Library/Application Support/Claude/Crashpad/`

---

**Note:** The LaunchServices timeout errors are the primary indicator of the crash cause. Addressing the LaunchServices database corruption or compatibility issues should resolve the crashes.

