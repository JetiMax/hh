#Test


import unittest
import allure
import httpx
import requests
from pytest_httpx import HTTPXMock


def test_post_status_codes(httpx_mock: HTTPXMock):
    httpx_mock.add_response(method="POST")

    with httpx.Client() as client:
        response = client.post("https://httpbin.org/#/operations/Status%20codes/post_status__codes_")
        print(response)


def test_post(httpx_mock: HTTPXMock):
    httpx_mock.add_response(method="POST")

    with httpx.Client() as client:
        response = client.post("https://httpbin.org/post")
        print(response)


def test_put(httpx_mock: HTTPXMock):
    httpx_mock.add_response(method="PUT")

    with httpx.Client() as client:
        response = client.put("https://httpbin.org/put")
        print(response)


def test_delete(httpx_mock: HTTPXMock):
    httpx_mock.add_response(method="DELETE")

    with httpx.Client() as client:
        response = client.delete("https://httpbin.org/delete")
        print(response)


def test_patch(httpx_mock: HTTPXMock):
    httpx_mock.add_response(method="PATCH")

    with httpx.Client() as client:
        response = client.patch("https://httpbin.org/patch")
        print(response)


def test_head(httpx_mock: HTTPXMock):
    httpx_mock.add_response(method="HEAD")

    with httpx.Client() as client:
        response = client.head("https://httpbin.org/head")
        print(response)


def test_status_code():
    with allure.step("Запрос отправлен, посмотрим код ответа"):
        response = requests.get("https://httpbin.org/get")
        assert response.status_code == 200, f"Неверный код ответа, получен {response.status_code}"
        with allure.step("Запрос отправлен. Десериализируем ответ из json в словарь."):
            response = response.json()
            with allure.step(f"Посмотрим что получили {response}"):
                print(response)


if __name__ == '__main__':
    unittest.test()
