// version-checker.ts
import { execSync } from "child_process";

function checkPackageVersion(pkg: string) {
  try {
    const result = execSync(`npm list ${pkg} version --depth=0`, { encoding: "utf-8" });
    console.log(`📦 ${pkg}: ${result}`);
  } catch (err) {
    console.error(`❌ Could not find version for package: ${pkg}`);
  }
}

function checkGlobalPackageVersion(pkg: string) {
  try {
    const result = execSync(`npm list -g ${pkg} version --depth=0`, { encoding: "utf-8" });
    console.log(`🌍 (Global) ${pkg}: ${result}`);
  } catch (err) {
    console.error(`❌ Could not find global version for package: ${pkg}`);
  }
}

const packageName = process.argv[2];

if (!packageName) {
  console.log("Usage: ts-node version-checker.ts <package-name>");
  process.exit(0);
}

console.log("🔎 Checking package version...\n");

checkPackageVersion(packageName);
checkGlobalPackageVersion(packageName);
